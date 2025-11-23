# Question Paper Generator

## supplier 
https://code-projects.org/question-paper-generator-in-php-with-source-code/
## Vulnerability file
signupscript.php

## describe

**Code analysis**   

In the signupscript.php file of Question Paper Generator, the Fname parameter is obtained, and the SQL statement is concatenated to the SQL statement without filtering the execution, resulting in SQL injection vulnerabilities and server permissions

Line 32-41 in signupscript.php

```php
 $query="INSERT INTO tbuser VALUES('$Fname','$Lname','$contact','$collg','$board','$email','$passwd','$address','$country','$desc','$type')";
 if (mysqli_query($conn, $query))
 {
 echo "Congrats "."$Fname"." "."$Lname"."  Now you are the registred user..!!";
 }
 else
 {
  die(mysqli_error($conn));
 }
mysqli_close($conn);
```

## POC

```
POST /exam/signupscript.php HTTP/1.1
Host: 127.0.0.1:8083
Content-Length: 157
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
Referer: http://127.0.0.1:8083/exam/Signup.php
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close

Fname=123456&Lname=12345645&contact=123456&collg=&board=12356456&email=12312312&passwd=312312345&address=123456456465&country=123456456&desc=123&type=teacher
```

**Result**
![image-2025](https://github.com/asd1238525/cve/blob/main/2bdf15dd-d51c-461a-99c2-afde0d0c47a6.png)
Get payload:
![image-2025](https://github.com/asd1238525/cve/blob/main/9e20e5f2-e1dc-4caa-940c-aeabf06ee936.png)