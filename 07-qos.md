# QoS

QoS의 개념, traffic classification/marking, congestion management를 정리한 문서입니다.

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
