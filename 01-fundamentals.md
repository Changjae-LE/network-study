# Network Fundamentals

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

OSI 계층별 대표 장비 / 주소
| 계층 | 주요 주소/정보 | 대표 장비 |
| --- | --- | --- |
| Layer 4 | Port Number | Firewall, Load Balancer |
| Layer 3 | IP Address | Router, L3 Switch |
| Layer 2 | MAC Address | Switch, Bridge |
| Layer 1 | Bit / Signal | Cable, Hub, Repeater |

| TCP/IP 계층       | OSI 모델과의 관계                                    |
| ----------------- | ---------------------------------------------------- |
| Application Layer | OSI의 Application, Presentation, Session 계층에 해당 |
| Transport Layer   | OSI의 Transport 계층에 해당                          |
| Internet Layer    | OSI의 Network 계층에 해당                            |
| Link Layer        | OSI의 Data Link, Physical 계층에 해당                |

TCP/IP 핵심
| 개념 | 설명 |
| --- | --- |
| TCP/IP | 인터넷에서 사용하는 핵심 프로토콜 |
| TCP | 신뢰성 있는 연결 지향 통신 |
| UDP | 빠르지만 신뢰성 보장이 없는 비연결형 통신 |
| IP | 목적지까지 Packet을 전달하기 위한 주소 체계 |

PDU(Protocol Data Unit)
| 계층 | 데이터 단위 이름 |
| --- | --- |
| Application Layer | Data |
| Transport Layer | Segment |
| Internet / Network Layer | Packet |
| Link / Data Link Layer | Frame |

## PDU & Encapsulation

| OSI 계층  | PDU 이름 | Encapsulation 과정                   |
| --------- | -------- | ------------------------------------ |
| Layer 7~5 | Data     | 애플리케이션 데이터                  |
| Layer 4   | Segment  | TCP/UDP 헤더 추가                    |
| Layer 3   | Packet   | IP 헤더 추가                         |
| Layer 2   | Frame    | MAC 헤더 추가                        |
| Layer 1   | Bits     | 0과 1의 비트로 물리 매체를 통해 전송 |

핵심:

- Encapsulation은 송신자가 위 계층에서 아래 계층으로 내려가며 헤더를 붙이는 과정이다.
- Decapsulation은 수신자가 아래 계층에서 위 계층으로 올라가며 헤더를 제거하는 과정이다.

Transport Layer
Transport Layer는 호스트 간 데이터 전송을 관리하는 계층
| 역할 | 설명 |
| --- | --- |
| End-to-end 데이터 전송 | 송신자와 수신자 사이의 데이터 전달 관리 |
| Error recovery | 데이터 손실이나 오류 발생 시 복구 지원 가능 |
| Flow control | 수신자가 감당할 수 있도록 송신 속도 조절 가능 |
| Session multiplexing | 여러 통신 세션을 동시에 구분하고 관리 |
| Port number 사용 | 어떤 애플리케이션으로 보낼 데이터인지 구분 |

Physical Layer
Layer 1, Physical Layer는 실제 데이터를 bitstream, 즉 0과 1의 비트 형태로 물리 매체에 실어 보내는 계층

Ethernet / Cable
| 개념 | 설명 |
| --- | --- |
| Ethernet | 가장 많이 사용되는 유선 LAN 기술 |
| UTP | 일반적인 LAN 케이블 |
| STP | 차폐 기능이 있는 케이블 |
| 10Base-T | 10Mbps, Baseband, Twisted Pair |
| 100Base-TX | Fast Ethernet |
| 1000Base-T | Gigabit Ethernet |

10Base-T 의미:
| 부분 | 의미 |
| --- | --- |
| 10 | 속도 10Mbps |
| Base | Baseband |
| T | Twisted Pair |

라우터와 스위치 차이
| 구분 | 라우터 | 스위치 |
| --- | --- | --- |
| 주요 계층 | Layer 3 | Layer 2 |
| 주요 역할 | 서로 다른 IP subnet 간 트래픽 전달 | 같은 LAN 안의 호스트 간 트래픽 전달 |
| 인식 정보 | IP 주소 | MAC 주소 |
| 인터페이스 종류 | Ethernet, Serial, ISDN, ADSL 등 다양함 | 보통 Ethernet |
| 포트 수 | 보통 적음 | 보통 많음 |
| Broadcast 처리 | 기본적으로 전달하지 않음 | Broadcast traffic을 전달함 |

Data Link Layer

MAC Address
| 항목 | 설명 |
| --- | --- |
| 계층 | Layer 2 |
| 크기 | 48 bits |
| 표기 | 12자리 16진수 |
| 앞 24 bits | OUI, 제조사 식별 |
| 뒤 24 bits | 장비 고유 식별자 |

핵심:

- Switch는 MAC Address Table을 사용한다.
- MAC Address는 같은 LAN 안에서 통신할 때 사용된다.

Traffic Types
| 방식 | 설명 |
| --- | --- |
| Unicast | 하나의 목적지에게 전송 |
| Broadcast | 같은 네트워크의 모든 장비에게 전송 |
| Multicast | 특정 그룹에게 전송 |

Broadcast MAC Address:
FFFF.FFFF.FFFF

핵심:

- ARP는 Broadcast를 사용한다.
- Switch는 Broadcast를 같은 VLAN 안의 모든 포트로 전달한다.
- Router는 Broadcast를 다른 네트워크로 전달하지 않는다.

Switch Operation
| 동작 | 설명 |
| --- | --- |
| Learning | Source MAC Address를 MAC Address Table에 저장 |
| Flooding | 목적지 MAC을 모르면 들어온 포트를 제외하고 전체 전송 |
| Forwarding | 목적지 MAC을 알면 해당 포트로만 전송 |
| Filtering | 불필요한 포트로 Frame을 보내지 않음 |
| Aging | 오래된 MAC Address Table 항목 삭제 |

핵심:

- Switch는 Source MAC Address를 보고 학습한다.
- Unknown Unicast는 Flooding된다.
- Broadcast는 Flooding된다.

Network Layer

IP Address
| 개념 | 설명 |
| --- | --- |
| IPv4 | 32-bit 주소 체계 |
| IPv6 | 128-bit 주소 체계 |
| Subnet Mask | Network 부분과 Host 부분을 구분 |
| Default Gateway | 다른 네트워크로 나갈 때 사용하는 Router 주소 |
| DHCP | IP 주소를 자동으로 할당하는 프로토콜 |
| ARP | IP 주소를 MAC 주소로 변환하는 프로토콜 |

핵심:

- 같은 네트워크의 장비들은 같은 Network ID를 가진다.
- 다른 네트워크로 통신하려면 Default Gateway가 필요하다.
- ARP는 IP 주소를 MAC 주소로 바꿀 때 사용한다.

Collision Domain / Broadcast Domain
| 개념 | 설명 |
| --- | --- |
| Collision Domain | 동시에 전송하면 충돌이 발생할 수 있는 범위 |
| Broadcast Domain | Broadcast가 전달되는 범위 |

장비별 특징:
| 장비 | Collision Domain | Broadcast Domain |
| --- | --- | --- |
| Hub | 나누지 못함 | 나누지 못함 |
| Switch | 포트별로 나눔 | 기본적으로 나누지 못함 |
| Router | 나눔 | 나눔 |

핵심:

- Switch는 Collision Domain을 나눈다.
- Router는 Broadcast Domain을 나눈다.
- VLAN은 Switch에서 Broadcast Domain을 나누는 기술이다.

Switch Loop / STP
| 개념 | 설명 |
| --- | --- |
| Loop | Frame이 네트워크 안에서 계속 순환하는 현상 |
| Broadcast Storm | Broadcast Frame이 반복되어 네트워크가 마비되는 현상 |
| STP | Switch Loop를 방지하기 위한 프로토콜 |
| EtherChannel | 여러 개의 링크를 하나처럼 묶는 기술 |

핵심:

- STP는 중복 경로 중 일부 포트를 차단해 Loop를 방지한다.
- 장애가 발생하면 차단된 경로를 다시 사용할 수 있다.
- EtherChannel은 여러 링크를 하나의 논리적 링크처럼 사용한다.
