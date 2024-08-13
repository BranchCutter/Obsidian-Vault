## 사전 준비
* 호환되는 리눅스 머신.
* 2GB 이상의 램을 장착한 머신
  (이 보다 작으면 사용자의 앱을 위한 공간이 거의 남지 않음)
* 2개 이상의 CPU 코어
* 클러스터의 모든 머신에 걸친 네트워크 연결
* 모든 노드에 대해 고유한 호스트 이름, MAC 주소 및 product_uuid
	* `ip link` 또는 `ifconfig -a` 명령으로 네트워크 인터페이스의 MAC 주소 확인 가능
	* `sudo cat /sys/class/dmi/id/product_uuid` 명령을 사용하여 product_uuid 확인 가능
* 컴퓨터의 특정 포트들 개방
	* 필수 포트들은 쿠버네티스 컴포넌트들이 서로 통신하기 위해서 열려 있어야 함
		* `ufw allow 6443`
	* netcat과 같은 도구를 이용하여 포트가 열려 있는지 확인해볼 수 있음
		* `nc 127.0.0.1 6443 -v`
	* 사용자가 사용하는 특정 파드 네트워크 플러그인이 요구하는 특정 포트를 열어야 할 수 있음
		* 필요한 포트에 대한 플러그인 문서를 참조
* Swap의 비활성화. kubelet이 제대로 작동하게 하려면 반드시 Swap을 사용하지 않도록 설정
	* `sudo swapoff -a` // swap off
	* `free -h` // check swap off
	* `sudo sed -i '/ swap / s/^\(.*\)$/#\1/g' /etc/fstab/` // maintain swap settings after rebooting

---
### 컨테이너 런타임 설치
* 파드에서 컨테이너를 실행하기 위해, 쿠버네티스는 컨테이너 런타임을 사용
* 쿠버네티스는 컨테이너 런타임 