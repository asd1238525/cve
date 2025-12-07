# Question Paper Generator

## supplier 
https://code-projects.org/question-paper-generator-in-php-with-source-code/
## Vulnerability file
login.php

## describe

**Code analysis**   

In the login.php file of Question Paper Generator, the username parameter is obtained, and the SQL statement is concatenated to the SQL statement without filtering the execution, resulting in SQL injection vulnerabilities and server permissions

Line 2-12 in login.php

```php
POST /attend/SimpleAttendanceRecord/admin/login.php HTTP/1.1
Host: 127.0.0.1:8083
Content-Length: 24
sec-ch-ua: 
Accept: */*
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
sec-ch-ua-mobile: ?0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.5845.97 Safari/537.36
sec-ch-ua-platform: ""
Origin: http://127.0.0.1:8083
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: cors
Sec-Fetch-Dest: empty
Referer: http://127.0.0.1:8083/attend/SimpleAttendanceRecord/admin/
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=3dcksdlknmh19ka49it8b8skf4
Connection: close

username=11&password=111
```

## POC

```
POST /attend/SimpleAttendanceRecord/admin/login.php HTTP/1.1
Host: 127.0.0.1:8083
Content-Length: 24
sec-ch-ua: 
Accept: */*
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
sec-ch-ua-mobile: ?0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.5845.97 Safari/537.36
sec-ch-ua-platform: ""
Origin: http://127.0.0.1:8083
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: cors
Sec-Fetch-Dest: empty
Referer: http://127.0.0.1:8083/attend/SimpleAttendanceRecord/admin/
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=3dcksdlknmh19ka49it8b8skf4
Connection: close

username=11&password=111
```

**Result**
![image-2025](https://github.com/asd1238525/cve/blob/main/5b54c81e-d922-4d0c-bdf8-2eaafa0445ec.png)
Get payload:
![image-2025](https://github.com/asd1238525/cve/blob/main/6798c051-56eb-4a66-ba01-e5a6a7299f4c.png)