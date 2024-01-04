## Container Orchastration

> 컨테이너 오케스트레이션은 컨테이너의 배포, 관리, 확장, 네트워킹을 자동화한다.

```
컨테이너 오케스트레이션은 컨테이너를 사용하는 어떤 환경에서든 사용할 수 있다.
또한 재설계할 필요 없이 각기 다른 환경 전반에 동일한 애플리케이션을 배포하는 데에도 도움이 됨
컨테이너에 마이크로서비스를 구현하면 스토리지, 네트워킹, 보안과 같은 서비스를
간편하게 오케스트레이션 할 수 있다.
```

컨테이너는 마이크로서비스 기반 애플리케이션에 이상적인 애플리케이션 배포 유닛 및 독립적인 실행 환경을 제공한다.
동일한 하드웨어의 마이크로서비스에서 애플리케이션의 여러 부분들을 독립적으로 실행시키고 개별 요소 및 라이프 사이클을 더욱 효과적으로 제어할 수 있다.

오케스트레이션을 통해 컨테이너 라이프사이클을 관리하면 CI/CD 워크플로우에 이를 통합하는 DevOps 팀을 지원할 수도 있다.
컨테이너화된 마이크로서비스는 API(Application Programing Interface) 및 DevOps 팀과 함께 Cloud Native Application의 기반을 이루게 된다.

### Where does Container Orchastration use?

```
Using Container Orchastration
 ├─ Provisioning and deployment
 ├─ Organize and schedule
 ├─ Resource allocation
 ├─ Container availability
 ├─ Scale or remove container based on workload balancing across infrastructure
 ├─ Load Balancing and Traffic Routing
 ├─ Monitor container health
 ├─ Set up an application based on the container that will run
 └─ Secure container-to-container interactions
```

### Container Orchastration Tools
컨테이너 오케스트레이션 툴은 컨테이너와 마이크로 서비스 아키텍처를 규모에 따라 관리할 프레임워크를 제공한다. 컨테이너 라이프사이클 관리에 사용할 수 있는 컨테이너 오케스트레이션 툴은 다양하며 그 중 Kubernetes, Docker Swarm, Apache Mesos가 널리 사용된다.

Kubernetes는 원래 Google 엔지니어들이 개발하고 설계한 오픈소스 컨테이너 오케스트레이션 툴이다.
2015년에 Google은 새로 설립된 Cloud Native Computing Foundation에 쿠버네티스 프로젝트를 donation했다.

쿠버네티스 오케스트레이션을 사용하면 여러 컨테이너에 걸쳐 애플리케이션 서비스를 구축하고 클러스터 전체에서 컨테이너의 일정을 계획하고 이러한 컨테이너를 확장하여 컨테이너의 상태를 지속적으로 관리할 수 있다.

쿠버네티스에서는 애플리케이션 컨테이너를 배포하고 확장하는데 수동 프로세스가 대부분 필요하지 않다.
Linux 컨테이너를 실행하는 호스트 그룹(물리적 머신 또는 가상 머신 모두 가능)을 함께 클러스터링 할 수 있으며 쿠버네티스를 통해 이러한 클러스터를 쉽고 효율적으로 관리할 수 있다.

더 넓게 보면, 프로덕션 환경에 컨테이너 기반 인프라를 완전히 구현해서 사용할 수 있다.

클러스터는 퍼블릭, 프라이빗 또는 하이브리드 클라우드 전체로 호스트를 확장할 수 있다.
이러한 이유로 쿠버네티스는 신속한 확장을 요하는 클라우 네이티브 애플리케이션을 호스팅하는 데 이상적인 플랫폼이다.

또한 재설께 필요 없이 애플리케이션을 이동할 수 있도록 지원하므로 워크로드 이식성과 로드 밸런싱에도 도움이 된다.

```
Key components of Kubernetes
 ├─ Cluster
 │  └─ A control plane and one or more compute machines or nodes.
 ├─ Control plane
 │  └─ A collection of processes that control Kubernetes nodes.
 │     This is where all task assignments begin.
 ├─ Kublet
 │  └─ This service runs on the node, reads the container manifest,
 │     and verifies that the defined container is up and running.
 └─ Pod
    └─ A group of one or more containers deployed on single node.
       All containers in pod share an IP, IPC, hostname, and other resources.
```

