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

