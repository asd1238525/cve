# Simple Pizza Ordering System

## supplier 
https://code-projects.org/simple-pizza-ordering-system-in-php-with-source-code-2/
## Vulnerability file
request.php

## describe

**Code analysis**   

In the request.php file of Question Paper Generator, the name parameter is obtained, and the SQL statement is concatenated to the SQL statement without filtering the execution, resulting in SQL injection vulnerabilities and server permissions

Line 59-69 in save_student_query.php

```php
	if(isset($_POST['name']) && $_POST['name'] != "" && isset($_POST['contact']) && $_POST['contact'] != ""){
		require_once("session.php");
		require_once("db.php");

		$db = new Db();
		$sess = new Session();

		$or = $db->placeOrder($_POST['name'], $_POST['contact'], $sess->getCart());
		echo "success:+:".$or;
		//$sess->endSession();
	}
```

## POC

```
POST /pizzaorder/simple-pizza-order/src/request.php HTTP/1.1
Host: 127.0.0.1:8083
Content-Length: 28
sec-ch-ua: 
Accept: */*
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
sec-ch-ua-mobile: ?0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.5845.97 Safari/537.36
sec-ch-ua-platform: ""
Origin: http://127.0.0.1:8083
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: cors
Sec-Fetch-Dest: empty
Referer: http://127.0.0.1:8083/pizzaorder/simple-pizza-order/order.php
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=l076ipd3qhcavev8ehp8ihb3kk
Connection: close

place-order&name=1&contact=1
```

**Result**
![image-2025](https://github.com/asd1238525/cve/blob/main/5bfb4bfd-a7cf-4838-9855-6fa6b7f7609c.png)
Get payload:
![image-2025](https://github.com/asd1238525/cve/blob/main/000383b2-ee4b-45ac-80f2-210cbc864b78.png)