## CNI(Container Network Interface)

* Container간 통신을 지원하는 VxLAN. Pod Network이라고도 부름
* *pod와 pod간의 통신을 위해 필수*
* 다양한 종류의 플러그인이 존재
* ex) 플라넬(flannel), 칼리코(calico), 위브넷(weavenet) 등

---
## Configure of Kubernetes cluster

```
control plane(master node)
 ├─ Manage and control the state of worker nodes
 ├─ Single master
 └─ Multi master(3, 5개의 master nodes)

worker node
 └─ Operate containers through the Docker platform and provide actual services
```