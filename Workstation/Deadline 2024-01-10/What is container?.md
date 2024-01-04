## Container
``` js
# cat > app.js
const http = require('http');
const os = require('os');
console.log("test server starting..");
var handler = function(req, res) {
	res.writeHead(200);
	res.end( "Container Hostaname:" + os.hostname() + "\n");
}
var www = http.createServer(handler);
www.listen(8080);
```

``` docker
# cat > Dockerfile
FROM node:12
COPY app.js /app.js
ENTRYPOINT ["node", "app.js"]
```

#### How to make Container?
* webserver 컨테이너 생성

![400](https://i.imgur.com/ieHmQvH.png)
