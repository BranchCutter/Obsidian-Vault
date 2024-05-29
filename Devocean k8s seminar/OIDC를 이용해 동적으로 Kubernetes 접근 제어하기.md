
Index
* Native Kubernetes 접근 제어 방식
* OIDC를 활용한 Kubernetes 접근 제어 방식
* TKS의 Kubernetes 접근 제어 방식
* 기술 구성
	* 인증
		* 인증 개요
		* JWT Token
		* Open ID Connect(OIDC)
	* 인가
		* 인가 개요
		* Kubernetes RBAC 구성


---
## Kubernetes 접근 제어하기

![](https://i.imgur.com/IKDtq13.png)

여러 사용자들이 존재하고 그들이 중요시하는 자원들이 각각 다름

---
## Native Kubernetes 접근 제어 방식

![](https://i.imgur.com/M5Fgl51.png)

Kubeconfig

```
Cluster :
 -  cluster URL
 -  certificate-authority-data
User:
 -  token
```

- 기존의 토큰 회수 어려움

---
## OIDC를 활용한 Kubernetes 접근 제어 방식

![](https://i.imgur.com/MR7y851.png)

Service 별 토큰이 아니라 모든 역할에 대한 Kubeconfig 파일이 동일하게 떨어짐

```
Cluster:
 -  cluster URL
 -  certificate-authority-data
User:
 -  exec:
 -  - oidc-plugin
```

---
## OIDC plugin 동작방식
![](https://i.imgur.com/goMTWgu.jpeg)

---
## 인증 (Authentication)

사용자가 서버에게 자신이 누구인지를 증명하는 과정

주요 Step
- 자격 증명: 사용자는 자신의 신원을 증명하기 위해 자격 증명을 제출
- 신우너 검증: 제출된 자격 증명 정보를 기존에 등록된 계정 정보와 비교하여 사용자의 신원을 확인
- 결과 전송: 검증이 성공하면 사용자는 인증된 것으로 간주되어 시스템에 접근할 수 있는 인증 토큰 발급
- 인증 토큰 검증: 제출된 인증 토큰 유효성 검증 & 신원 확인

-> 개인화된 서비스 제공

### Json Web Token(JWT)

Header : 토큰 타입과 서명 알고리즘 정보 포함
Payload: 사용자 정보 및 클레임 포함
	iss (Issuer): 토큰을 발행한 인증 서버의 URL
	iat (Issued At): 토큰이 발행된 시간
	exp (Expiration Time): 토큰의 만료 시간
	aud (Audience): 토큰의 수신자를 식별
	sub (Subject): 토큰의 주체로, 사용자에 대한 고유 식별자
Signature: 헤더와 페이로드를 인코딩하고, 비밀 키로 전자 서명하여 변조 방지

### OpenID Connect

ID Token 이라는 JWT를 사용하여 최종 사용자 신원 정보를 전달하는 인증 프로토콜

- 신원 정보 claim
- Custom claim

---
## 인가 (Authorization)

- 인증된 사용자가 어떤 작업을 수행할 수 있는지를 결정하는 과정
-
- 권한(Permission)
	- 특정 사용자가 특정 자원에 대해 어떤 작업을 수행할 수 있는지를 결정하는 규칙
	- Match
		- 주체, 행위
		- HTTP의 경우, 일반적으로 HTTP 요청에 첨부된 Token, Method, PATH를 활용
	- Action
		- 허용
- 권한 관리 방식
	- ABAC
	- RBAC

=> 인증/인가 동작 흐름
1. 자격 증명
2. Tkn 전송
3. HTTP 요청 w/Token
4. public key 요청


---
초기 설정
Auth Server
	Kubernetes에 대한 OIDC 설정
		Client 설정
			Client-id
			ID Token Claim 설정
				k8s-groups

Kubernetes
	Auth Server에 대한 OIDC 설정
		Auth Server URL
		Client-id
		Custom Claim 필드 설정
			--oidc-groups-claim-k8s-groups

관리
	Auth Server
		사용자 관리
		Client 설정
			역할 관리
		{user-client-role} 매핑 관리
		역할 별 Custom 권한 설정
	Kubernetes
		역할 별 ClusterRole/Role Binding 관리
		역할에 관계된 ClusterRole/Role 관리

