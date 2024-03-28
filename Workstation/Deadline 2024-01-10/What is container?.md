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

---
### Container Hierarchy

Layer 6
 ├─ Development Workflow Opinionated Containers
 └─ OpenShift, Cloud Foundary, Docker Cloud, Deis, Flynn ...
 Layer 5
  ├─ Orchestration/Scheduling Service Model
  └─ Kubernetes, Docker Swarm, Marathon/Mesos, Nomad, Diego
 Layer 4
 ├─ Conatiner Engine
 └─ Docker, Rocket, RunC(OCI), Osv, LXC, LXD
Layer 3
 ├─ Operating System
 └─ Ubuntu, RHEL, CoreOS, Unikernels
Layer 2
 ├─ Virtual Infrastructure
 └─ vSphere, EC2, GCP, Azure, OpenStack
Layer 1
 ├─ Physical Infrastructure
 └─ Raw Computer, Network, Storage

---
### Kubernetes.io

그리스어 : 조타수
2014년 구글에서 사용하던 컨테이너 오케스트레이션 시스템 "보그"를 오픈 소스화 한 것
10년 이상 대규모 시스템 운영 경험을 녹여서 출시 발표

#### k8s

* 워크로드 분리
* 어디서나 실행가능 - 온프레미스, 퍼블릭 클라우드(AKS, EKS, GKE 등)
* *선언적 API*

---
