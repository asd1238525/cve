# Simple E-Banking System #

## supplier ##

https://code-projects.org/simple-e-banking-system-in-php-with-source-code/

## Vulnerability file ##

register.php

## describe ##

The `register.php` file contains an unrestricted cross-site scripting (XSS) vulnerability, leading to a stored XSS attack. Malicious attackers can exploit this vulnerability to obtain sensitive information from the client side.

### Code analysis ###

Line 32 in register.php

```php
		while($row = mysqli_fetch_array($query))
		{
			$table_user=$row['username'];
			if($username==$table_user)
			{
				$bool=false;
				Print '<script>alert("Username has already been taken!");</script>';
				Print '<script>window.location.assign("register.php");</script>';
			}
		}
		if($bool)
		{
			mysqli_query($conn, "INSERT INTO users (username,password) VALUES ('$username','$password')");
			Print '<script>alert("Successfully Registered! ");</script>';
			Print '<script>window.location.assign("index.php");</script>';
		}
```

## POC ##
For id parameter, the test payload is `<script>alert(1)</script>`
Visit this URL to trigger the cross-site scripting vulnerability.

```
http://127.0.0.1:8083/bank/eBank/register.php
```

### Rusult ###
![image](https://github.com/asd1238525/cve/blob/main/ade199b2-4566-487e-aa4c-39937df3cb4d.png)
![image](https://github.com/asd1238525/cve/blob/main/331d6e43-80c4-4d53-8b53-84970562c328.png)
For parameter "username":
![image](https://github.com/asd1238525/cve/blob/main/ae3482ff-12aa-437a-9e9d-d5468dced80e.png)
