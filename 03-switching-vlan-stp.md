# Switching, VLAN, and STP

Data-Link Layer, LAN 구조, VLAN, Trunk, STP, EtherChannel, CAM/Flooding을 정리한 문서입니다.

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

CDP and LLDP
| 구분 | CDP | LLDP |
| --- | --- | --- |
| 표준 여부 | Cisco 전용 | Open standard |
| 기본 활성화 | Cisco 장비에서 보통 기본 활성화 | 장비/버전에 따라 다름 |
| 동작 계층 | Layer 2 | Layer 2 |
| 지원 인터페이스 | 물리 인터페이스 + 일부 가상 sub-interface | 물리 인터페이스만 |
| 포트당 탐지 | 여러 장비 탐지 가능 | 포트당 하나의 장비만 탐지 |
| Linux 서버 탐지 | 불가 | 가능 |

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

CAM(Content Addressable Memory)
스위치가 “어떤 MAC 주소가 어느 포트에 연결되어 있는지” 기억해두는 표, MAC address table이라고도 불려짐

Flooding은 스위치가 프레임의 목적지 MAC 주소를 CAM table에서 찾지 못했을 때, 그 프레임을 받은 포트를 제외한 모든 포트로 뿌리는 과정
