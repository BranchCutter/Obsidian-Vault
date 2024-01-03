### Pod
```
Pod는 하나 이상의 컨테이너로 구성된 그룹이며 쿠버네티스의 기본 빌딩 블록
```

```
Pod는 항상 두 개 이상의 컨테이너를 포함하는 것을 의미하지 않는다.
일반적으로 pod는 하나의 컨테이너만 포함한다.
```

```
모든 컨테이너는 항상 하나의 워커 노드에서 실행되며
여러 워커 노드에 걸쳐 시행되지 않는다.
```

![](https://i.imgur.com/VJlCRxM.jpg)

All Containers of a pod run on the same node. A pod never spans two nodes.

### Why does pod need?

> Multi Process Single Container vs Single Process Multi Container

컨테이너는 단일 프로세스를 실행하는 것을 목적으로 설계되었다.
(Process가 Children Process를 생성하는 것은 제외)

여러 Process를 실행하는 Single Container의 단점
* Single Container에서 관련이 없는 다른 프로세스를 실행하는 경우 모든 프로세스를 실행하고 로그를 관리하는 것은 모두 사용자 책임이다.
* 모든 프로세스는 동일한 Standard Output으로 로그를 기록하기에 어떤 프로세스가 남긴 로그인지 파악을 하는 것이 어렵다.
-> 이에 각 프로세스를 자체 개별 컨테이너로 실행해야 하는 것을 권장한다.

> [!faq] 그렇다면 컨테이너를 직접 이용하지 않고 왜 pod이라는 개념이 존재하는가?
> pod 내부에 존재하는 컨테이너가 Running할 수 있ㅆ는 동일한 환경을 제공하면서 독립성을 보존할 수 있는 Container보다 상위 레벨의 그룹이 요구되었다.
> Container Group(=pod)를 사용하여 밀접하게 연관된 프로세스를 함께 실행하고 단일 컨테이너 안에서 모두 함께 실행 되는 것처럼 동일한 환경을 제공할 수 있으면서도 이들은 격리된 상태로 유지할 수 있다.

### Understanding Pod
pod를 이용함으로써 아래와 같은 기여효과를 얻는다.
1. 컨테이너가 제공하는 모든 기능을 활용하는 동시 프로세스가 함께 실행
2. 이들을 격리된 상태로 유지

pod를 통해 컨테이너가 제공하는 모든 기능을 활용하는 동시 프로세스가 함께 실행하고 단일 컨테이너 안에서 모두 함께 실행되는 것처럼 동일한 환경을 제공할 수 있으면서도 이들을 격리된 상태로 유지할 수 있다.

### Partial isolation between containers in the same pod

pod 안에 있는 컨테이너가 특정한 리소스를 공유하기 위해 각 컨테이너가 완벽하게 격리되지 않도록 한다. 쿠버네티스는 pod 안에 있는 모든 컨테이너가 자체 네임스페이스가 아닌 동일한 리눅스 네임스페이스를 공유하도록 도커를 설정한다.

* 모든 컨테이너는 동일한 네트워크 네임스페이스와 UTS 네임스페이스 안에서 실행되기 때문에 모든 컨테이너는 같은 호스트 이름과 네트워크 인터페이스를 공유한다.
* 모든 컨테이너는 동일한 IPC 네임스페이스 아래에서 실행되어 IPC를 통해 서로 통신할 수 있다.
* 최근 동일한 PID 네임스페이스를 공유할 수 있지만 기본적으로 활성화 되어 있지 않다.
* Filesystem에 한해서는 조금 다르다. 대부분 컨테이너 파일 시스템은 컨테이너 이미지에서 나오기에, 파일시스템은 다른 컨테이너와 완전히 분리된다.

> *UTS namespace(Unix Timesharing System)*
> system의 *hostname을 namespace 별로 격리*시켜 준다.
> Linux System Call인 uname에서 struct에 정의된 식별자 중 nodename을 isolate하는 것이다.

> *IPC namespace(Inter-ProcessCommunication)*
> *프로세스간 서로 데이터를 주고 받는 경로*를 의미한다.
> Linux에서 사용되는 대표적인 IPC 방식은 Signal, Socket, pipe 등이 있다.
> 이러한 IPC resource를 격리 시켜 제공한다.

---
### How containers share the same IP and port space

pod안의 컨테이너가 동일한 네트워크 네임스페이스에서 실행되기에 동일한 IP 주소와 포트 공간을 공유한다.
* 동일한 파드 안 컨테이너에서 실행 중인 프로세스가 같은 포트 번호를 사용하지 않도록 주의
* 다른 pod 경우 서로 다른 포트 공간을 가지기에 포트 충돌이 일어나지 않는다.
* pod 안에 있는 모든 컨테이너는 동일한 루프백 네트워크 인터페이스를 가지기에 컨테이너들이 Localhost를 통해 서로 통신할 수 있다.

---
## Flat Network between Pod

파드는 논리적인 호스트로서 컨테이너가 아닌 환경에서의 물리적 호스트 혹은 VM과 유사하게 동작

* 클러스터의 모든 Pod는 하나의 Flat한 공유 네트워크 주소 공간에 상주한다.
* 모든 Pod는 다른 Pod의 IP 주소를 사용하여 접근하는 것이 가능하다.
(Pod간 어떠한 NAT도 존재하지 않으며 마치 LAN처럼 통신이 가능하다.)
* Pod 안에 있는 모든 컨테이너는 동일한 루프백 네트워크 인터페이스를 가지기에 컨테이너들이 Localhost 