# Network Services

DNS, ARP, DHCP, FHRP, HSRP를 정리한 문서입니다.

DNS (Domain Name System)
FQDN(Fully Qualified Domain Name)을 IP 주소로 변환하는 시스템

ARP(Address Resolution Protocol)
IP 주소를 MAC 주소로 바꿔주는 역할
ARP Request는 Layer 2 broadcast이다 -> broadcast는 라우터를 넘어가지 않음
따라서 다른 subnet으로 통신할 때는 default gateway(라우터)의 MAC주소를 ARP로 찾는다

DNS를 통해 FQDN을 IP 주소로 변환하는 과정
1. 웹사이트 이름 입력
2. Host가 DNS Server에 IP 주소 물어봄
3. 다른 subnet이면 Router를 거쳐 감
4. 각 구간에서 MAC 주소를 모르면 ARP 사용
5. DNS Server가 IP 주소를 응답
6. Host가 목적지 IP를 알게 됨
7. 이제 실제 웹 요청 시작 가능

DNS로 목적지 IP를 알아낸 뒤, 실제 HTTP 웹 트래픽이 Host A에서 Web Server까지 이동하는 과정
1. Host A가 DNS로 Web Server IP를 알아냄
2. Host A가 HTTP 요청 생성
3. 목적지가 다른 subnet이므로 Router A로 보냄
4. Router A가 routing table을 보고 Router B로 보냄
5. Router B가 Web Server가 있는 subnet으로 전달
6. Web Server가 HTTP 요청을 수신
7. 이후 패킷은 ARP 없이 더 빠르게 전달

DHCP Server 구성 방식
| 방식 | 설명 |
| --- | --- |
| Cisco Router 사용 | 라우터가 DHCP 서버 역할 수행 |
| External Server 사용 | Windows, Linux, Unix 서버 등을 DHCP 서버로 사용 |

FHRP = First Hop Redundancy Protocols
여러 gateway router가 하나의 가상 default gateway처럼 동작하게 해주는 프로토콜
FHRP 종류
| 프로토콜 | 특징 |
| --- | --- |
| HSRP | Cisco 전용, Active/Standby 방식 |
| VRRP | Open Standard, Active/Standby 방식 |
| GLBP | Cisco 전용, Active/Active Load Balancing 지원 |

HSRP = Hot Standby Router Protocol
HSRP는 Cisco의 gateway 이중화 프로토콜입니다.
여러 라우터가 하나의 Virtual IP와 Virtual MAC address를 공유해서, PC 입장에서는 하나의 default gateway만 있는 것처럼 보이게 합니다.

HSRP에서는 priority로 Active Router를 정하고, preemption으로 복구된 preferred router가 다시 Active가 되게 할 수 있으며, 여러 HSRP group이나 subnet별 Active Router 분리를 통해 제한적인 load balancing도 구현할 수 있습니다.

Layer 3에서는 루프 방지와 장애 조치
주로 라우팅과 HSRP가 경로 선택과 자동 장애 조치를 담당
