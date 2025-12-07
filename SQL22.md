# Simple Attendance Record System

## supplier 
https://code-projects.org/simple-attendance-record-system-in-php-with-source-code/
## Vulnerability file
save_student_query.php

## describe

**Code analysis**   

In the save_student_query.php file of Question Paper Generator, the student_no parameter is obtained, and the SQL statement is concatenated to the SQL statement without filtering the execution, resulting in SQL injection vulnerabilities and server permissions

Line 3-17 in save_student_query.php

```php
	if(ISSET($_POST['save'])){
		$student_no = $_POST['student_no'];
		$firstname = $_POST['firstname'];
		$middlename = $_POST['middlename'];
		$lastname = $_POST['lastname'];
		$course = $_POST['course'];
		$section = $_POST['section'];
		$conn->query("INSERT INTO `student` VALUES('', '$student_no','$firstname', '$middlename', '$lastname', '$course', '$section')") or die(mysqli_error());
			echo '
				<script type = "text/javascript">
					alert("Saved Record");
					window.location = "student.php";
				</script>
			';
	}	
```

## POC

```
POST /attend/SimpleAttendanceRecord/admin/save_student_query.php HTTP/1.1
Host: 127.0.0.1:8083
Content-Length: 713
Cache-Control: max-age=0
sec-ch-ua: 
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: ""
Upgrade-Insecure-Requests: 1
Origin: http://127.0.0.1:8083
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryMsvtqCBFksQyxJss
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/116.0.5845.97 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Referer: http://127.0.0.1:8083/attend/SimpleAttendanceRecord/admin/student.php
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=3dcksdlknmh19ka49it8b8skf4
Connection: close

------WebKitFormBoundaryMsvtqCBFksQyxJss
Content-Disposition: form-data; name="student_no"

1
------WebKitFormBoundaryMsvtqCBFksQyxJss
Content-Disposition: form-data; name="firstname"

1
------WebKitFormBoundaryMsvtqCBFksQyxJss
Content-Disposition: form-data; name="middlename"

1
------WebKitFormBoundaryMsvtqCBFksQyxJss
Content-Disposition: form-data; name="lastname"

1
------WebKitFormBoundaryMsvtqCBFksQyxJss
Content-Disposition: form-data; name="course"

1
------WebKitFormBoundaryMsvtqCBFksQyxJss
Content-Disposition: form-data; name="section"

1
------WebKitFormBoundaryMsvtqCBFksQyxJss
Content-Disposition: form-data; name="save"


------WebKitFormBoundaryMsvtqCBFksQyxJss--

```

**Result**
![image-2025](https://github.com/asd1238525/cve/blob/main/a3dc5a8e-cf19-496d-bff7-4f76a3583b66.png)
Get payload:
![image-2025](https://github.com/asd1238525/cve/blob/main/fc3849c4-7d35-492a-9126-62a6ded32078.png)