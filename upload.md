# Responsive Blog Site #

## supplier ##

https://code-projects.org/simple-food-ordering-system-in-php-with-source-code/

## Vulnerability file ##

editproduct.php

## describe ##

The editproduct.php file contains an unrestricted file upload vulnerability, allowing attackers to upload arbitrary files (such as webshells) to the server. Malicious attackers can exploit this vulnerability to gain remote code execution or further compromise the system.

### Code analysis ###

Line 1-29 in editproduct.php

```php
include('conn.php');

$id=$_GET['product'];

$pname=$_POST['pname'];
$category=$_POST['category'];
$price=$_POST['price'];

$sql="select * from product where productid='$id'";
$query=$conn->query($sql);
$row=$query->fetch_array();

$fileinfo=PATHINFO($_FILES["photo"]["name"]);

if (empty($fileinfo['filename'])){
$location = $row['photo'];
}
else{
$newFilename=$fileinfo['filename'] ."_". time() . "." . $fileinfo['extension'];
move_uploaded_file($_FILES["photo"]["tmp_name"],"upload/" . $newFilename);
$location="upload/" . $newFilename;
}

$sql="update product set productname='$pname', categoryid='$category', price='$price', photo='$location' where productid='$id'";
$conn->query($sql);

header('location:product.php');
```

## POC ##
For the file upload vulnerability, you can upload a malicious PHP file (such as a webshell) using the product edit functionality. The application does not validate the file type or content, allowing arbitrary files to be uploaded to the server.

```
http://127.0.0.1:8083/foodorder/ordersimple/product.php
```

### Rusult ###
![image](https://github.com/asd1238525/cve/blob/main/1e9f175b-7fae-41ce-9582-29c2b6d52d4e.png)
For parameter "id":
![image](https://github.com/asd1238525/cve/blob/main/b32871b3-b057-4574-a27c-3f635cfc8185.png)
