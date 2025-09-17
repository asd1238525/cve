# Responsive Blog Site #

## supplier ##

https://code-projects.org/simple-food-ordering-system-in-php-with-source-code/

## Vulnerability file ##

order.php

## describe ##

The `order.php` file contains an unrestricted cross-site scripting (XSS) vulnerability, leading to a stored XSS attack. Malicious attackers can exploit this vulnerability to obtain sensitive information from the client side.

### Code analysis ###

Line 17-27 in order.php

```php
$sql="select * from product left join category on category.categoryid=product.categoryid order by product.categoryid asc, productname asc";
$iterate=0;
while($row=$query->fetch_array()){
<tr>
<td class="text-center"><input type="checkbox" value="<?php echo $row['productid']; ?>||<?php echo $iterate; ?>" name="productid[]" style=""></td>
<td><?php echo $row['catname']; ?></td>
<td><?php echo $row['productname']; ?></td>
<td class="text-right">&#x20A8; <?php echo number_format($row['price'], 2); ?></td>
<td><input type="text" class="form-control" name="quantity_<?php echo $iterate; ?>"></td>
</tr>
```

## POC ##
For id parameter, the test payload is `"><script>alert(1)</script>`
Visit this URL to trigger the cross-site scripting vulnerability.

```
http://127.0.0.1:8083/foodorder/ordersimple/order.php
```

### Rusult ###
![image](https://github.com/asd1238525/cve/blob/main/4328a7d60ac7e12a59747ca6c605d8b4.png)
For parameter "id":
![image](https://github.com/asd1238525/cve/blob/main/fb381e7d-9408-42e2-b076-a5d433af0cd4.png)
