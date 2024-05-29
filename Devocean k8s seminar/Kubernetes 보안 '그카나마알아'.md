---
SKT: 한규호
---
---
# K8S Security
#그카나마알아
#SKT

---
## K8S Security == REST API Security
REpresentional State 
![](https://i.imgur.com/X23x1nH.png)

내가 원하는 바를 업데이트 하는 것

=> 쿠버네티스는 API 서버라는 것

---
## API Internal : AuthN, AuthZ & Admission

![](https://i.imgur.com/QN6P8dB.png)


REST API 보안?

---
## Authentication

인증 : 대상이 스스로 주장하는 신원을 확인하는 행위
신원증명 수단 : **X.509** or **ID Token**

---
## Authentication : X.509
Public Key Digital Signature : 인증서 배포/공개키 배포는 알아서 잘 해야됨(?)

---
## Authentication

인증 대상이 고정된 경우 : X.509 (kube-scheduler)
인증 대상이 다이나믹한 경우 : ID Token (User, Pod)

---
## Admission : Policy Enforcement for Governance
