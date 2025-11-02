# Student Information System #

## supplier ##

https://code-projects.org/student-information-system-in-php-with-source-code-2/

## Vulnerability file ##

editprofile.php

## describe ##

The `editprofile.php` file contains firstname parameter an unrestricted cross-site scripting (XSS) vulnerability, leading to a stored XSS attack. Malicious attackers can exploit this vulnerability to obtain sensitive information from the client side.

### Code analysis ###

Line 8-30 in editprofile.php

```php
  if(isset($_POST['update'])) {

    $fname = clean($_POST['firstname']);
    $lname = clean($_POST['lastname']);
    $course = clean($_POST['course']);
    $yrlevel = clean($_POST['yrlevel']);

    $query = "UPDATE students SET firstname = '$fname', lastname = '$lname', course = '$course', yrlevel = '$yrlevel'
    WHERE id='".$_SESSION['userid']."'";

    if($result = mysqli_query($con, $query)) {

      $_SESSION['prompt'] = "Profile Updated";
      header("location:profile.php");
      exit;

    } else {

      die("Error with the query");

    }
  }
```

## POC ##
For username parameter, the test payload is `<script>alert(document.cookie)</script>`
Use this payload to update firstname, then log in; every time you log in, the cookie will be popped.

### Rusult ###
![image](https://github.com/asd1238525/cve/blob/main/b8c137c43f0c82017231721ee1b6c832.png)
For parameter "firstname":
![image](https://github.com/asd1238525/cve/blob/main/cfa759af32a911d227151382c4546830.png)
