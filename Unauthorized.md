# Automated Voting System #

https://code-projects.org/automated-voting-system-in-php-with-source-code/

## Vulnerability file ##

vote.php sess.php

## describe ##

The `vote.php` file includes `sess.php`, which allows direct access to the backend by bypassing the login process simply by accessing the `vote.php` file. This vulnerability enables attackers to tamper with data and cause data leakage.

### Code analysis ###

Line 2-12 in sess.php

```php
require 'admin/dbcon.php';
session_start(); 
if(!ISSET($_SESSION['voters_id'])){
//header("location:index.php");
}else{
$session_id=$_SESSION['voters_id'];
$user_query = $conn->query("SELECT * FROM user WHERE user_id = '$session_id'") or die(mysqli_errno());
$user_row = $user_query->fetch_array();
$user_username = $user_row['firstname']." ".$user_row['lastname'];
}
```

Line 2 in vote.php

```php
include("sess.php");
```

## POC ##
For the target, directly accessing the `vote.php` file after the `/automated voting` directory.

```
http://127.0.0.1:8083/voting/automated%20voting/vote.php
```

### Rusult ###
The `sess.php` file is included in the `vote.php` file, which allows direct access to the backend by bypassing the login process.
![image-2025-06-15](https://github.com/asd1238525/cve/blob/main/images/20250615173615.png)
