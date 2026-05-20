# Device Basics and Management

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

Cisco DNA Center
Cisco 네트워크 장비들을 중앙에서 관리하고 자동화하는 컨트롤러/관리 플랫폼

- 네트워크 장비 중앙 관리
- 장비 설정 자동 배포
- 정책 기반 네트워크 운영
- 네트워크 상태 모니터링
- 보안 정책 적용
- 장비 프로비저닝
