# Network Security

Switch Security, DHCP Snooping, DAI, 802.1X, Port Security를 정리한 문서입니다.

Switch Security
DHCP Snooping
: 가짜 DHCP 서버(Rogue DHCP Server)가 클라이언트에게 잘못된 IP 설정을 주는 것을 막는 스위치 보안 기능
DHCP Snooping은 이를 막기 위해 스위치 포트를 두 종류로 나눈다.
| 구분 | 설명 |
| --- | --- |
| Trusted Port | 정상 DHCP 서버가 연결된 포트 또는 DHCP 서버 방향으로 가는 포트 |
| Untrusted Port | 일반 PC, 사용자 장비가 연결되는 포트 |
DAI(Dynamic ARP Inspection)
: 스위치가 ARP 정보를 검사해서 “이 IP 주소를 이 MAC 주소가 쓰는 게 맞는지” 확인하고, 거짓이면 차단하는 기능

802.1X Identity-Based Networking
802.1X는 사용자가 네트워크에 접속하기 전에 먼저 인증을 받도록 하는 보안 기능
802.1X 구성요소
| 구성요소 | 설명 |
| --- | --- |
| Supplicant | 사용자의 PC. 802.1X 인증을 요청하는 장비 |
| Authenticator | Access Layer Switch. 사용자가 연결되는 스위치 |
| Authentication Server | 사용자 인증을 처리하는 서버 |
동작 과정
| 1. | 사용자가 PC를 Access Switch에 연결한다. |
| --- | --- |
| 2. | 아직 인증되지 않았기 때문에 일반 네트워크에는 접근할 수 없다. |
| 3. | 인증 서버와 통신하는 트래픽만 허용된다. |
| 4. | 사용자가 username과 password를 입력한다. |
| 5. | 스위치가 이 정보를 authentication server로 전달한다. |
| 6. | Authentication server가 username과 password가 유효한지 확인한다. |
| 7. | 보통 authentication server는 Active Directory 같은 사용자 데이터베이스와 연동된다. |
| 8. | 인증이 성공하면, authentication server가 사용자에게 맞는 VLAN 정보를 스위치에 전달한다. |
| 9. | 스위치는 해당 포트를 올바른 VLAN에 배정한다. |
| 10. | 이후 사용자는 정상적으로 네트워크에 접근할 수 있다. |

Switch Port Security
: 스위치의 특정 포트에 들어올 수 있는 MAC 주소를 제한하는 보안 기능
동작 방식 세 가지
| Violation Mode | 동작 |
| --- | --- |
| shutdown | 기본값. 위반 발생 시 포트를 error-disabled 상태로 만들고 모든 트래픽 차단 |
| protect | 허용되지 않은 MAC 주소의 트래픽만 차단. 허용된 MAC 주소의 트래픽은 계속 전달 |
| restrict | 허용되지 않은 MAC 주소의 트래픽을 차단하고, 로그 기록 및 violation counter 증가 |

MAC learning function
스위치가 어떤 MAC 주소가 어느 포트에 연결되어 있는지 자동으로 학습하는 기능
- 스위치는 프레임의 출발지 MAC 주소를 보고,
- 그 MAC 주소가 들어온 포트와 연결되어 있다는 것을
- MAC 주소 테이블 또는 CAM 테이블에 저장한다.
