---
SKT: 임상일
---
---
## 인증과 인가를 넘어서

인증(Authentication)을 통해 사용자의 신원, 소속 부서 등의 정보를 확인
인가(Authorization)를 통해 사용자가 접근할 수 있는 시스템이나 자원(Resource)을 정의하고 가능한 행위(API Call)를 통제
정책은 인가를 포함한 더 넓은 범위
	권한이 아닌 정책의 예: 네이밍룰, 세션관리
정책의 필요성
	RBAC은 유사한 권한을 Role로 관리함

---
## Kubernetes의 정책 관련 지원 기능
PSP(Pod Security Policies) : Pod에 정의하여 행위를 제한
Network Policy : 네트워크 트래픽을 제한
Admission Policy
	v1.30(24.04)에서 추가
	CEL (Common Expression Language)

---
## Kubernetes Admission Controller

![](https://i.imgur.com/NBDXnuv.png)

---
## Kubernetes용 정책 관리 도구

Kyverno
OPA Gatekeeper
OPA
Istio

---
## 정책관리별 장단점 비교

![](https://i.imgur.com/Tj22vR9.png)

---
