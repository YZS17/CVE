# Stored XSS vulnerability in unmark v1.9.3 of file /info.php

**vender**:

- [cdevroe/unmark: An open source to do app for bookmarks.](https://github.com/cdevroe/unmark)

**SoftLink**:

- [Release 1.9.3 · cdevroe/unmark](https://github.com/cdevroe/unmark/releases/tag/v1.9.3)

**Vulnerable File**

- application/controllers/Marks.php
- application/views/marks/info.php

**Version**

- 2.8.0

### Analyse

Stored XSS Vulnerability Analysis

This stored XSS vulnerability exists in two key files:

1. Vulnerability Injection Point: `application/controllers/Marks.php`

In the controller, the system retrieves the webpage title from a user-provided URL without performing any HTML escaping or filtering:

```php
// Around lines 42-54
$dom = new DOMDocument();
libxml_use_internal_errors(true);
if (!$dom->loadHTMLFile($url, LIBXML_NOWARNING)) {
    // Error handling...
} else {
    $list = $dom->getElementsByTagName("title");
    if ($list->length > 0) {
        $title = $list->item(0)->textContent; // Title retrieved here without filtering
    }
}
```

2. Vulnerability Trigger Point: `application/views/marks/info.php`

In the view file, line 28 directly outputs the unfiltered title:

```php
<h1 class="hideoutline"><?php print $mark->title; ?></h1>
```

The code uses `print` to directly output the variable instead of using `htmlspecialchars()` or other secure output methods.

### Exploitation Process

1. An attacker creates an svg page containing malicious  JavaScript in its title
2. The attacker induces a victim to submit this malicious URL through the application's "Add Bookmark" feature
3. The application retrieves the page title and stores it in the database, along with the malicious code
4. When the victim or other users view the bookmark details page, the malicious JavaScript code is executed

### Complete Attack Chain

The complete attack chain is:

1. Attacker creates an svg page with malicious JavaScript in its title
2. Victim adds this URL via the `/marks/add` interface
3. The system uses `DOMDocument::loadHTMLFile()` to get the page title without filtering
4. The malicious title is stored in the database
5. When users visit the `/mark/info/{mark_id}` page, the malicious JavaScript executes

### POC

put a `xss1.svg`  on vps

```
<?xml version="1.0" standalone="no"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "
http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
<svg version="1.1" baseProfile="full" xmlns="http://www.w3.org/2000/svg">
<polygon id="triangle" points="0,0 0,50 50,0" fill="#009900" stroke="#004400
"/>
<script type="text/javascript">
alert('xss');
</script>
</svg>
```



![image-20250829011240326](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508290112531.png)

- click it

![image-20250829011433219](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508290114733.png)

then xss

![image-20250829011443239](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508290114438.png)
