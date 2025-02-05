```php
<?php
function gen_secured_random() { // cause random is the way
    $a = rand(1337,2600)*42;
    $b = rand(1879,1955)*42;

    $a < $b ? $a ^= $b ^= $a ^= $b : $a = $b;

    return $a+$b;
}

function secured_hash_function($plain) { // cause md5 is the best hash ever
    $secured_plain = sanitize_user_input($plain);
    return md5($secured_plain);
}

function sanitize_user_input($input) { // cause someone told me to never trust user input
    $re = '/[^a-zA-Z0-9]/';
    $secured_input = preg_replace($re, "", $input);
    return $secured_input;
}

if (isset($_GET['source'])) {
    show_source(__FILE__);
    die();
}


require_once "secret.php";

if (isset($_POST['s']) && isset($_POST['h'])) {
    $s = sanitize_user_input($_POST['s']);
    $h = secured_hash_function($_POST['h']);
    $r = gen_secured_random();
    if($s != false && $h != false) {
        if($s.$r == $h) {
            print "Well done! Here is your flag: ".$flag;
        }
        else {
            print "Fail...";
        }
    }
    else {
        print "<p>Hum ...</p>";
    }
}
?>
```
To make the condition `$s.$r == $h` right, I need to use PHP type juggling
- `$s` A user-provided seed, sanitized by sanitize_user_input(), which removes all non-alphanumeric characters.
- `$h` Another user input that is hashed using md5(), ensuring the comparison involves an MD5 hash.
- `$r` A randomly generated number.

Read this [document](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20PHP%20loose%20comparison%20-%20Type%20Juggling%20-%20OWASP.pdf), discoverd that when comparing a string to a number, PHP will attempt to
convert the string to a number then perform a numeric
comparison. Example: `"0e12" == int(0)`


So the goal is that, I need to find the `h` value that got its hashed value start with `0e`. This way, when `$s.$r` is also `0e...`, PHP treats both as 0, making the condition `$s.$r == $h` true.

The `h` values can be found in [this](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Type%20Juggling/README.md)
```
s=0e&h=QNKCDZO&submit=Check
```
Flag: `F34R_Th3_L0o5e_C0mP4r15On`