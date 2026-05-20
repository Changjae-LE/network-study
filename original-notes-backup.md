# Original Network Notes Backup

OSI 7계층
| 계층 | 이름 | 주요 내용 |
| --- | --- | --- |
| Layer 7 | Application | 이메일 같은 애플리케이션 데이터 |
| Layer 6 | Presentation | 데이터 표현 관련 계층 |
| Layer 5 | Session | 세션 관련 계층 |
| Layer 4 | Transport | TCP/UDP, 포트 번호 |
| Layer 3 | Network | 출발지/목적지 IP 주소, 라우터 |
| Layer 2 | Data Link | MAC 주소, 스위치 |
| Layer 1 | Physical | 실제 전송 매체, 케이블 등 |

| TCP/IP 계층 | OSI 모델과의 관계 |
| --- | --- |
| Application Layer | OSI의 Application, Presentation, Session 계층에 해당 |
| Transport Layer | OSI의 Transport 계층에 해당 |
| Internet Layer | OSI의 Network 계층에 해당 |
| Link Layer | OSI의 Data Link, Physical 계층에 해당 |

PDU(Protocol Data Unit)
| 계층 | 데이터 단위 이름 |
| --- | --- |
| Application Layer | Data |
| Transport Layer | Segment |
| Internet / Network Layer | Packet |
| Link / Data Link Layer | Frame |

| 계층 | 이름 |
| --- | --- |
| Layer 7~5 | Data |
| Layer 4 | Segment |
| Layer 3 | Packet |
| Layer 2 | Frame |

Transport Layer
Transport Layer는 호스트 간 데이터 전송을 관리하는 계층
| 역할 | 설명 |
| --- | --- |
| End-to-end 데이터 전송 | 송신자와 수신자 사이의 데이터 전달 관리 |
| Error recovery | 데이터 손실이나 오류 발생 시 복구 지원 가능 |
| Flow control | 수신자가 감당할 수 있도록 송신 속도 조절 가능 |
| Session multiplexing | 여러 통신 세션을 동시에 구분하고 관리 |
| Port number 사용 | 어떤 애플리케이션으로 보낼 데이터인지 구분 |

Network Layer
Layer 3, Network Layer는 패킷을 목적지까지 보내기 위한 라우팅을 담당
| 프로토콜 | 설명 |
| --- | --- |
| IP | 가장 대표적인 Layer 3 프로토콜 |
| ICMP | ping 같은 문제 해결에 사용 |
| IPSec | 암호화된 보안 통신에 사용 |

Routing Table에 들어가는 경로
| Route 종류 | 의미 |
| --- | --- |
| Connected route | 라우터 인터페이스에 직접 연결된 네트워크 |
| Local route | 라우터 인터페이스에 설정된 실제 IP 주소 |
| Static route | 관리자가 직접 설정한 경로 |
| Dynamic route | 라우팅 프로토콜로 자동 학습한 경로 |

Data-Link Layer
Layer 2, Data-Link Layer는 데이터를 실제 물리 계층으로 보내기 전에 frame 형태로 만들고, 물리 계층에서 온 bit들을 다시 해석하는 역할, Ethernet이 가장 많이 사용됨

Ethernet Header 구성
| 필드 | 설명 |
| --- | --- |
| Preamble | 송신자와 수신자가 동기화하는 데 사용 |
| Destination MAC Address | 목적지 MAC 주소 |
| Source MAC Address | 출발지 MAC 주소 |
| Ethertype | Ethernet 안에 어떤 프로토콜이 들어있는지 표시, 예: IPv4 |
| Data | 실제 데이터 |
| FCS | Frame Check Sequence, 프레임 손상 여부 확인 |

Physical Layer
Layer 1, Physical Layer는 실제 데이터를 bitstream, 즉 0과 1의 비트 형태로 물리 매체에 실어 보내는 계층

라우터와 스위치 차이
| 구분 | 라우터 | 스위치 |
| --- | --- | --- |
| 주요 계층 | Layer 3 | Layer 2 |
| 주요 역할 | 서로 다른 IP subnet 간 트래픽 전달 | 같은 LAN 안의 호스트 간 트래픽 전달 |
| 인식 정보 | IP 주소 | MAC 주소 |
| 인터페이스 종류 | Ethernet, Serial, ISDN, ADSL 등 다양함 | 보통 Ethernet |
| 포트 수 | 보통 적음 | 보통 많음 |
| Broadcast 처리 | 기본적으로 전달하지 않음 | Broadcast traffic을 전달함 |

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

CDP and LLDP
| 구분 | CDP | LLDP |
| --- | --- | --- |
| 표준 여부 | Cisco 전용 | Open standard |
| 기본 활성화 | Cisco 장비에서 보통 기본 활성화 | 장비/버전에 따라 다름 |
| 동작 계층 | Layer 2 | Layer 2 |
| 지원 인터페이스 | 물리 인터페이스 + 일부 가상 sub-interface | 물리 인터페이스만 |
| 포트당 탐지 | 여러 장비 탐지 가능 | 포트당 하나의 장비만 탐지 |
| Linux 서버 탐지 | 불가 | 가능 |

핵심 메모리 종류
| 메모리 | 역할 |
| --- | --- |
| ROM | 장비 전원을 켰을 때 처음 실행되는 기본 코드 저장 |
| Flash | IOS 운영체제 이미지 저장 |
| NVRAM | startup-config 저장 |
| RAM | 현재 실행 중인 IOS와 running-config가 올라가는 작업 메모리 |

부팅 순서
1. 전원 켜짐
2. ROM에서 POST 실행
3. Bootstrap 실행
4. Flash에서 IOS 이미지 찾기
5. IOS를 RAM으로 로드
6. NVRAM에서 startup-config 찾기
7. startup-config를 RAM으로 로드해서 running-config로 사용
8. 장비 정상 부팅 완료

ROM의 역할
1. POST 실행
2. Bootstrap 로드

Flash: IOS system image가 저장되어 있음
NVRAM: startup-config가 저장되어 있음

running-config와 startup-config 차이
| 설정 파일 | 저장 위치 | 의미 |
| --- | --- | --- |
| running-config | RAM | 현재 적용 중인 설정 |
| startup-config | NVRAM | 다음 부팅 때 적용될 설정 |

Routing Protocol의 큰 분류
Routing Protocol은 크게 두 가지로 나눌 수 있습니다.
| 구분 | 의미 | 사용 위치 |
| --- | --- | --- |
| IGP | Interior Gateway Protocol | 조직 내부 네트워크 라우팅 |
| EGP | Exterior Gateway Protocol | 조직 간, 인터넷 라우팅 |
IGP는 회사나 조직 내부에서 라우터들이 경로를 교환할 때 사용합니다.
EGP는 조직과 조직 사이, 특히 인터넷에서 라우팅할 때 사용합니다.

IGP의 종류
현재 사용되는 대표적인 IGP는 다음과 같습니다.
| 프로토콜 | 전체 이름 | 종류 |
| --- | --- | --- |
| RIP | Routing Information Protocol | Distance Vector |
| EIGRP | Enhanced Interior Gateway Routing Protocol | Distance Vector |
| OSPF | Open Shortest Path First | Link State |
| IS-IS | Intermediate System to Intermediate System | Link State |
Distance Vector 방식에서는 각 라우터가 직접 연결된 이웃 라우터에게 자신이 알고 있는 네트워크 목록과 그 네트워크까지의 거리를 알려줌
Link State 방식에서는 각 라우터가 자기 자신과 자신의 인터페이스 정보를 이웃 라우터에게 알려줌
| 구분 | Distance Vector | Link State |
| --- | --- | --- |
| 정보 기준 | 이웃 라우터의 관점 | 전체 네트워크 구조 |
| 전달 내용 | “나는 이 네트워크까지 이 거리로 갈 수 있음” | “네트워크에 이런 라우터와 링크가 있음” |
| 전체 토폴로지 인식 | 없음 | 있음 |
| 특징 | 단순하지만 정보가 제한적 | 더 정확하지만 부하가 더 큼 |
| 별명 | Routing by rumor | 전체 지도 기반 라우팅 |

Routing Protocol 선택 기준
| 프로토콜 | Metric | 특징 |
| --- | --- | --- |
| RIP | Hop Count | 단순하지만 bandwidth 고려 안 함 |
| OSPF | Cost | bandwidth 기반으로 좋은 경로 선택 |
| IS-IS | Cost | 기본적으로 모든 link cost 동일 |
| EIGRP | Bandwidth + Delay | 보통 좋은 경로를 자동 선택 |

ECMP(Equal Cost Multi Path)
목적지까지 가는 여러 경로의 metric이 같을 때, 라우터가 그 경로들을 모두 routing table에 넣고 트래픽을 분산하는 기능

Administrative Distance
| Route 종류 / Protocol | AD 값 | 선호도 |
| --- | --- | --- |
| Connected Interface | 0 | 가장 높음 |
| Static Route | 1 | 매우 높음 |
| External BGP | 20 | 높음 |
| EIGRP | 90 | IGP 중 가장 높음 |
| OSPF | 110 | RIP보다 높음 |
| IS-IS | 115 | OSPF보다 낮음 |
| RIP | 120 | 낮음 |

Loopback Interface를 사용하는 이유
| 사용 목적 | 설명 |
| --- | --- |
| 장비 관리 | SSH, Telnet 등으로 라우터에 접속할 때 사용 |
| BGP Peering | BGP 이웃 관계를 맺을 때 사용 |
| VoIP | 라우터로 들어오는 음성 트래픽에 사용 가능 |
| OSPF Router ID | OSPF에서 라우터를 식별하는 ID로 사용 |

Adjacency란?
Adjacency는 같은 routing protocol을 사용하는 라우터들이 서로 이웃 관계를 맺고, routing update를 교환할 수 있는 상태

Routing Protocol이 활성화된 인터페이스의 동작
| 동작 | 설명 |
| --- | --- |
| Hello packet 송수신 | 이웃 라우터를 찾아 adjacency 형성 |
| Subnet 광고 | 해당 인터페이스의 subnet을 routing update에 포함 |

라우터가 route를 배우는 방법
| 방법 | 설명 |
| --- | --- |
| Connected Route | 인터페이스에 IP 주소를 설정하면 자동 생성 |
| Local Route | 인터페이스에 설정된 실제 IP 주소에 대한 /32 route |
| Static Route | 관리자가 직접 설정 |
| Dynamic Route | RIP, OSPF, EIGRP 같은 routing protocol을 통해 학습 |

라우터의 route 선택 순서(기준)
라우터가 패킷을 전달할 때는 목적지 IP 주소를 보고 routing table에서 가장 적절한 route를 찾습니다.
선택 기준은 다음 순서입니다.
1. Longest Prefix Match
2. Administrative Distance
3. Metric

계층별 troubleshooting 명령어
| 계층 | 명령어 / 도구 | 용도 |
| --- | --- | --- |
| Layer 1 | show ip interface brief | 인터페이스 상태 확인 |
| Layer 1 | show interface | 인터페이스 상세 상태 확인 |
| Layer 2 | show arp | IP와 MAC 매핑 확인 |
| Layer 2 | show mac address-table | 스위치 MAC 주소 테이블 확인 |
| Layer 4 | telnet [IP] [port] | 특정 포트 응답 확인 |
| DNS | nslookup | DNS 이름 해석 확인 |
| DNS | ping FQDN | 도메인 이름이 IP로 해석되는지 확인 |

RIP이란?
Distance Vector 방식으로 전체 네트워크 구조를 보는 것이 아니라, 이웃 라우터가 알려주는 정보를 바탕으로 경로를 학습함
RIP의 특징
| 항목 | 설명 |
| --- | --- |
| Protocol Type | Distance Vector |
| Metric | Hop Count |
| 최대 Hop Count | 15 |
| ECMP | 기본적으로 최대 4개 equal-cost path 지원 |
| 주 사용 환경 | Lab, demo, 매우 작은 네트워크 |

EIGRP(Enhanced Interior Gateway Routing Protocol)
IGRP의 발전된 형태이며, RIP보다 훨씬 빠르고 큰 네트워크에서도 사용할 수 있는 라우팅 프로토콜
EIGRP의 주요 특징
- RIP보다 convergence time이 빠름
- 네트워크 변화가 생겼을 때 관련된 라우터에게만 업데이트를 보내는 bounded update 지원
- 브로드캐스트가 아니라 멀티캐스트를 사용해 EIGRP 라우터끼리만 메시지 처리
- 기본적으로 최대 4개의 경로에 대해 equal cost load balancing 지원
- 다른 라우팅 프로토콜과 달리 unequal cost load balancing도 가능
- 단, unequal cost load balancing은 자동이 아니라 수동 설정이 필요함

OSPF Packet Types
| Packet | 의미 | 역할 |
| --- | --- | --- |
| Hello | 이웃 발견 | Neighbor를 찾고 adjacency 형성 |
| DBD | Database Descriptor | 자신이 알고 있는 네트워크 정보 요약 전달 |
| LSR | Link State Request | 부족한 정보 요청 |
| LSA | Link State Advertisement | 링크 상태 정보 전달 |
| LSU | Link State Update | 여러 LSA를 담아 업데이트 전달 |
| LSAck | Link State Acknowledgement | 받은 메시지에 대한 확인 응답 |

LAN
| 계층 | 역할 | 특징 |
| --- | --- | --- |
| Access Layer | End host 연결 | 높은 포트 수, 저렴한 비용, 보안 정책 적용 |
| Distribution Layer | Access switch 집약 | redundancy 구성, QoS 등 소프트웨어 정책 적용 |
| Core Layer | 건물/영역 간 연결 | 속도와 안정성 중심, 소프트웨어 정책 최소화 |

| 구분 | 전통적 Campus LAN | Spine-Leaf |
| --- | --- | --- |
| 계층 | Access / Distribution / Core | Leaf / Spine |
| 주 사용 환경 | 일반 사무실, 학교, 캠퍼스 LAN | 데이터센터 |
| 서버 연결 위치 | Access Layer | Leaf Layer |
| 중심 계층 | Core Layer | Spine Layer |
| 주요 트래픽 | North-South | East-West |
| 확장 방식 | 계층별 확장 | Spine 또는 Leaf 추가 |
| 특징 | 사용자 중심 네트워크에 적합 | 서버 간 통신에 적합 |

VLAN이란?
VLAN = Virtual Local Area Network
VLAN은 switch에서 사용하는 Layer 2 기능입니다.
VLAN의 핵심 역할은 LAN을 여러 개의 분리된 broadcast domain으로 나누는 것

VLAN이 필요한 이유
| 문제 | 설명 |
| --- | --- |
| 성능 문제 | 필요 없는 장비까지 broadcast traffic을 처리해야 함 |
| 보안 문제 | broadcast traffic이 router/firewall의 Layer 3 보안 정책을 우회할 수 있음 |
| 대역폭 낭비 | 필요 없는 링크와 스위치까지 traffic이 퍼짐 |

Access Port와 Trunk Port 차이
| 구분 | Access Port | Trunk Port |
| --- | --- | --- |
| 용도 | PC, 서버 같은 end host 연결 | 스위치 간 연결 |
| VLAN 처리 | 하나의 VLAN만 전달 | 여러 VLAN traffic 전달 |
| VLAN 태그 | 보통 태그 없음 | 802.1Q 태그 사용 |
| 예시 | PC가 연결된 포트 | Switch1 ↔ Switch2 연결 포트 |

DTP = Dynamic Trunking Protocol
Cisco 스위치끼리 연결되었을 때, 두 스위치 포트가 자동으로 trunk가 될지 협상하는 Cisco 전용 프로토콜
DTP 모드
| 설정 | 의미 |
| --- | --- |
| switchport mode access | 수동으로 access port 설정 |
| switchport mode trunk | 수동으로 trunk port 설정 |
| switchport mode dynamic auto | 상대가 trunk/desirable이면 trunk 형성 |
| switchport mode dynamic desirable | 적극적으로 trunk 협상 |
| switchport nonegotiate | DTP 비활성화 |

Inter-VLAN Routing 방식 1: Router Separate Interfaces
일반적으로 LAN에서는 하나의 VLAN이 하나의 IP subnet과 1:1로 연결됨

Router Separate Interfaces 방식
이 방식은 라우터의 물리 인터페이스를 VLAN마다 하나씩 사용하는 구조

Router on a Stick이란?
Router on a Stick은 라우터의 하나의 물리 인터페이스를 사용해서 여러 VLAN 간 라우팅을 처리하는 방식

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

Spanning Tree Protocol(STP)
Layer 2 스위치 네트워크에서 루프를 방지하는 기술
Layer 2에는 TTL이 없기 때문에 Layer 2 loop가 발생하면 프레임이 계속 순환할 수 있다. 이를 방지하기 위해 Spanning Tree Protocol(STP)을 사용한다.

PortFast
PortFast는 루프 가능성이 거의 없는 end host 포트를 STP 대기 시간 없이 즉시 forwarding 상태로 만드는 기능입니다

BPDU Guard
스위치는 Spanning Tree 정보를 담은 BPDU를 전송합니다. 일반 PC는 BPDU를 보내지 않습니다. 따라서 PortFast 포트에서 BPDU가 수신되면, “아 이 포트에 스위치가 연결됐구나”라고 판단하고 해당 포트를 즉시 error-disabled 상태로 shut down합니다.

Root Guard
의도하지 않은 스위치가 Spanning Tree의 Root Bridge가 되는 것을 막기 위해 Root Guard를 사용. Root Guard가 설정된 포트에서 현재 Root Bridge보다 더 우수한 BPDU를 받으면, 그 포트는 root-inconsistent 상태가 되고 트래픽을 전달하지 않음.

Spanning Tree BPDU Filter
BPDU Guard와 BPDU Filter 차이
| 기능 | 동작 |
| --- | --- |
| BPDU Guard | PortFast 포트에서 BPDU를 받으면 포트를 error-disabled 상태로 shutdown |
| BPDU Filter | BPDU를 보내지 않거나, 들어오는 BPDU를 무시함 |
BPDU Filter는 BPDU를 차단하거나 무시하는 기능이지만, 잘못 사용하면 Spanning Tree 보호 기능을 꺼버리는 것과 비슷해져서, 일반적으로 BPDU Filter는 권장되지 않음

Spanning Tree Loop Guard
Cisco의 Spanning Tree 기능 중 하나로, 주 목적은 Unidirectional Link, 즉 단방향 링크 장애로 인한 Layer 2 loop를 막는 기능

EtherChannel
: 여러 개의 물리적 링크를 하나의 논리적 링크처럼 묶는 기술

EtherChannel을 구성하는 방법
| 방식 | 설명 |
| --- | --- |
| LACP | 표준 프로토콜. 여러 벤더 장비에서 지원됨. 가장 권장되는 방식 |
| PaGP | Cisco 전용 프로토콜. LACP와 비슷하지만 Cisco proprietary라서 권장되지는 않음 |
| Static | 협상 없이 수동으로 EtherChannel을 구성하는 방식 |

Spanning Tree의 단점
일부 링크를 blocking 상태로 만들어 전체 대역폭을 다 쓰지 못할 수 있음
장애 발생 후 복구가 느릴 수 있음

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

IPv6 Addressing and Routing
IPv6 주소는 다음과 같은 형식으로 작성된다(16진수 표현).
2001:0DB8:0000:0001:0000:0000:0000:0001
앞 64비트 = 네트워크 주소(Prefix)
뒤 64비트 = 장비 주소(Interface ID)
| IPv6 주소 종류 | 설명 |
| --- | --- |
| Global Unicast | 인터넷에서 전역적으로 사용 가능한 주소 |
| Unique Local | 내부 네트워크용 주소 |
| Link Local | 같은 링크 안에서만 사용하는 주소 |

fe80::/10  → Link-Local
ff00::/8   → Multicast
fc00::/7   → Unique Local
2000::/3   → Global Unicast

| 종류 | 의미 |
| --- | --- |
| IPv6 Multicast | 하나의 패킷을 특정 그룹에 속한 여러 장비에게 전달 |
| IPv6 Anycast | 같은 주소를 가진 여러 장비 중 가장 가까운 장비 하나에게 전달 |

EUI-64 방식
: 보통 MAC 주소 48비트를 이용해서 IPv6의 뒤 64비트 Interface ID를 만드는 방식

IPv6 host가 주소를 받는 방법
| 방식 | 설명 |
| --- | --- |
| Static Addressing | 관리자가 직접 host에 IPv6 주소 설정 |
| DHCPv6 | DHCP 서버가 IPv6 주소를 할당 |
| SLAAC | host가 router 정보를 바탕으로 스스로 IPv6 주소 생성 |

SLAAC의 동작 방식
| 1. | Router interface에 Global Unicast IPv6 주소를 설정한다. |
| --- | --- |
| 2. | Router가 해당 link에 Router Advertisement를 보낸다. |
| 3. | Router Advertisement에는 /64 network prefix 정보가 포함된다. |
| 4. | Host는 그 prefix를 보고 자신의 IPv6 주소를 자동 생성한다. |
| 5. | Router는 자신을 default gateway로 사용하라고 host에게 알려준다. |

QoS(Quality of Service)
: 네트워크에서 중요한 트래픽에 더 좋은 서비스를 제공하는 기술
traffic classification/marking 방식
| 방식 | 계층 | 설명 |
| --- | --- | --- |
| CoS | Layer 2 | 802.1Q frame header에 표시 |
| DSCP | Layer 3 | IP header의 TOS byte 안에 표시 |
| ACL | Layer 3/4 | IP 주소, protocol, port 번호로 트래픽 식별 |
| NBAR | Layer 3~7 | 애플리케이션 특성을 깊게 분석해서 식별 |

QoS의 Congestion Management
: 라우터나 스위치에 혼잡이 발생했을 때 queue를 조정해서 중요한 트래픽에 더 좋은 서비스를 제공하는 것
| 방식 | 설명 |
| --- | --- |
| CBWFQ | Class-Based Weighted Fair Queueing. 특정 traffic class에 bandwidth 보장 |
| LLQ | Low Latency Queueing. CBWFQ에 priority queue를 추가한 방식 |

IPv6 주소 유형
| IPv6 주소 유형 | 범위/용도 | 예시 |
| --- | --- | --- |
| Global Unicast | 인터넷에서 사용 가능한 공인 IPv6 주소 | 2000::/3 |
| Link-local | 같은 링크, 같은 LAN 안에서만 사용 | FE80::/10 |
| Unique Local Address, ULA | 회사/조직 내부망용 사설 IPv6 | FC00::/7, 보통 FD00::/8 |
| Loopback | 자기 자신을 가리킴 | ::1 |
| Multicast | 여러 대상에게 한 번에 전송 | FF00::/8 |
| Unspecified | 아직 주소가 없음을 의미 | :: |
| Anycast | 여러 장비가 같은 주소를 공유하고, 가장 가까운 장비로 전달 | 일반 unicast 주소 형식 사용 |

CAM(Content Addressable Memory)
스위치가 “어떤 MAC 주소가 어느 포트에 연결되어 있는지” 기억해두는 표, MAC address table이라고도 불려짐

Flooding은 스위치가 프레임의 목적지 MAC 주소를 CAM table에서 찾지 못했을 때, 그 프레임을 받은 포트를 제외한 모든 포트로 뿌리는 과정

Cisco DNA Center
Cisco 네트워크 장비들을 중앙에서 관리하고 자동화하는 컨트롤러/관리 플랫폼
- 네트워크 장비 중앙 관리
- 장비 설정 자동 배포
- 정책 기반 네트워크 운영
- 네트워크 상태 모니터링
- 보안 정책 적용
- 장비 프로비저닝

Wires
Copper
- 전기 신호
PoE 가능
EMI/RFI 영향 받음
도청/tap 쉬움
STP/UTP twisted pair
conductor, bedding, sheathing
Single-mode fiber
- 장거리
9 microns
single wavelength / single path
DWDM
light reflection 적음
Multi-mode fiber
- 단거리 중심
장거리에서 감쇠 증가
여러 경로로 빛 이동
refraction/reflection 많음
손상에 취약