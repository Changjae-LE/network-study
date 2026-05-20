# Routing

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
