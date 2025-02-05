
On most PHP installations a filename longer than 4096 bytes will be cut off so any excess chars will be thrown away.
>This attack leverages PHP's internal handling of long file paths, specifically how paths exceeding a certain length (typically 4096 bytes) are silently truncated. This can bypass security controls in Local File Inclusion (LFI) vulnerabilities by altering the way file paths are resolved before reaching system calls.

Considering a php script:
```php
include("ch35/".$_GET['page'].".php");
```

Read more on this [document](https://repository.root-me.org/Exploitation%20-%20Web/EN%20-%20PHP%20path%20truncation.html)



Payload command: `echo 'a/../admin.html'$(printf '/.'%.0s {1..2027})'`

    