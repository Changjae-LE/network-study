# Network Fundamentals

OSI 7계층, TCP/IP 모델, PDU, Transport Layer, Physical Layer를 정리한 문서입니다.

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
