# RCE vulnerability in [RPi-Jukebox-RFID](https://github.com/MiczFlor/RPi-Jukebox-RFID) v2.8.0 of file /playsinglefile.php

**vender**:

- [MiczFlor/RPi-Jukebox-RFID: A Raspberry Pi jukebox, playing local music, podcasts, web radio and streams triggered by RFID cards, web app or home automation. All plug and play via USB. GPIO scripts available.](https://github.com/MiczFlor/RPi-Jukebox-RFID)

**SoftLink**:

- [Release v2.8.0: Fix Spotify Authentication · MiczFlor/RPi-Jukebox-RFID](https://github.com/MiczFlor/RPi-Jukebox-RFID/releases/tag/v2.8.0)

**Vulnerable File**

- /htdocs/api/playlist/playsinglefile.php

**Version**

- 2.8.0

### Vulnerability Principle

1. The script receives the `file` parameter via a GET request.
2. No filtering or escaping is applied to the `$file` variable.
3. `$file` is directly concatenated into the command string, wrapped only in single quotes.
4. In `common.php`, the `execScriptWithoutCheck()` function runs the command via `exec("sudo ".$absoluteCommand)`.

### Root Cause

1. Unlike the PUT-request handler, the GET-request handler does not use `str_replace("'","'\\''",...)` to escape single quotes.
2. An attacker can close the single quotes and append additional commands, achieving arbitrary command execution.

### POC (playsinglefile.php)

```http
GET /api/playlist/playsinglefile.php?file=test%27;id%3Epoc.txt;%27 HTTP/1.1
Host: 192.168.129.130
```

![image-20250828231640495](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508282316562.png)



![image-20250828231555631](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508282315754.png)