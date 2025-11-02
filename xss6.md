# Student Information System #

## supplier ##

https://code-projects.org/student-information-system-in-php-with-source-code-2/

## Vulnerability file ##

register.php

## describe ##

The `register.php` file contains an unrestricted cross-site scripting (XSS) vulnerability, leading to a stored XSS attack. Malicious attackers can exploit this vulnerability to obtain sensitive information from the client side.

### Code analysis ###

Line 9-56 in register.php

```php
  if(isset($_POST['register'])) {

    $uname = clean($_POST['username']); 
    $pword = clean($_POST['password']); 
    $studno = clean($_POST['studentno']); 
    $fname = clean($_POST['firstname']); 
    $lname = clean($_POST['lastname']); 
    $course = clean($_POST['course']); 
    $yrlevel = clean($_POST['yrlevel']); 

    $query = "SELECT username FROM students WHERE username = '$uname'";
    $result = mysqli_query($con,$query);

    if(mysqli_num_rows($result) == 0) {

      $query = "SELECT studentno FROM students WHERE studentno = '$studno'";
      $result = mysqli_query($con,$query);

      if(mysqli_num_rows($result) == 0) {

        $query = "INSERT INTO students (username, password, studentno, firstname, lastname, course, yrlevel, date_joined)
        VALUES ('$uname', '$pword', '$studno', '$fname', '$lname', '$course', '$yrlevel', NOW())";

        if(mysqli_query($con, $query)) {

          $_SESSION['prompt'] = "Account registered. You can now log in.";
          header("location:index.php");
          exit;

        } else {

          die("Error with the query");

        }

      } else {

        $_SESSION['errprompt'] = "That student number already exists.";

      }

    } else {

      $_SESSION['errprompt'] = "Username already exists.";

    }

  }
```

## POC ##
For username parameter, the test payload is `<script>alert(document.cookie)</script>`
Use this payload to register, then log in; every time you log in, the cookie will be popped.


### Rusult ###
![image](https://github.com/asd1238525/cve/blob/main/f6966c6b8a3f30c9f8da204396df63cb.png)
For parameter "username":
![image](https://github.com/asd1238525/cve/blob/main/35745b071a3b4f5c7dc5597c161ac816.png)
