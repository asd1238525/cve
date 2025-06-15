# Responsive Blog Site #

## supplier ##

https://code-projects.org/responsive-blog-site-in-php-with-source-code/

## Vulnerability file ##

search.php

## describe ##

The `search.php` file contains an unrestricted cross-site scripting (XSS) vulnerability, leading to a stored XSS attack. Malicious attackers can exploit this vulnerability to obtain sensitive information from the client side.

### Code analysis ###

Line 37-76 in search.php

```php
$search_keyword = '';
if(!empty($_POST['search']['keyword'])) {
$search_keyword = $_POST['search']['keyword'];
}
$sql = 'SELECT * FROM blogs WHERE title LIKE :keyword OR content LIKE :keyword  OR tags LIKE :keyword OR author LIKE :keyword ORDER BY id DESC ';
$per_page_html = '';
$page = 1;
$start=0;
if(!empty($_POST["page"])) {
$page = $_POST["page"];
$start=($page-1) * ROW_PER_PAGE;
}
$limit=" limit " . $start . "," . ROW_PER_PAGE;
$pagination_statement = $pdo_conn->prepare($sql);
$pagination_statement->bindValue(':keyword', '%' . $search_keyword . '%', PDO::PARAM_STR);
$pagination_statement->execute();
$row_count = $pagination_statement->rowCount();
if(!empty($row_count)){
$per_page_html .= "<div style='text-align:center;margin:20px 0px;'>";
$page_count=ceil($row_count/ROW_PER_PAGE);
if($page_count>1) {
for($i=1;$i<=$page_count;$i++){
if($i==$page){
$per_page_html .= '<input type="submit" name="page" value="' . $i . '" class="btn-page current btn-warning" />';
} else {
$per_page_html .= '<input type="submit" name="page" value="' . $i . '" class="btn-page btn-danger" />';
}
}
}
$per_page_html .= "</div>";
}
$query = $sql.$limit;
$pdo_statement = $pdo_conn->prepare($query);
$pdo_statement->bindValue(':keyword', '%' . $search_keyword . '%', PDO::PARAM_STR);
$pdo_statement->execute();
$result = $pdo_statement->fetchAll();
```

## POC ##
For id parameter, the test payload is `<script>alert(document.cookie)</script>`
Visit this URL to trigger the cross-site scripting vulnerability.

```
http://127.0.0.1:8083/resblog/resblog/search.php
```

### Rusult ###
![image](https://github.com/asd1238525/cve/blob/main/20250615191933.png)
For parameter "id":
![image](https://github.com/asd1238525/cve/blob/main/20250615-191848.png)
