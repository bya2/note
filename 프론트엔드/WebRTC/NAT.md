# NAT (Network Address Translation)

- 사설 IP를 공인 IP로 변경할 때 필요한 `주소 변환 서비스`
- 라우터 등의 장비를 사용해서 '다수의 사설 IP'를 '하나의 공인 IP' 주소로 변환하는 기술

#### 예(ex)

- 주로 기업이나 기관에서 내부망을 사용하는 PC에 사설 IP를 제공하고, 외부 인터넷 연결 시에 공인 IP 하나를 같이 사용하는 형태로 운영

## NAT Forwarding Table

다수의 주소 변환 정보에 대해 IP 주소와 PORT 번호로 구성된 테이블

#### 구성

- 내부 네트워크에 위치한 호스트들의 사설 IP와 포트 번호
- 외부로 나갈 때의 동일한 공인 IP와 각기 다른 포트 번호
- 목적지 주소의 공인 IP와 서비스에 사용된 동일한 서비스 포트 번호

## 필요

- 공인 IP 주소를 절약
- 제한된 수의 인터넷 IPv4 주소 문제 해결
- 보안
- 로컬 도메인 외부의 네트워크 망 구성방식을 다양한 방식으로 변경 가능

## 동작 원리

- `NAT 지원 라우터`를 사용하는 일반적인 네트워크 설정

  - 두 개의 네트워크 인터페이스(Private Network, Public Network)

- `NAT`의 일반적인 설정

- IP masquerading (마스쿼레이딩): 하나의 공인 IP 뒤로 여러 개의 사설 IP 공간을 은닉하는 기법

#### NAT의 프로세스

1. 클라이언트에서 TCP SYN을 웹 서버로 전송

2. 패킷이 `NAT 라우터`에 의해 `사설 네트워크 인터페이스`에서 수신되고, `아웃바운드 트래픽 규칙`이 패킷에 적용

- 발신자인 클라이언트의 주소가 NAT 라우터의 공용 IP 주소로 변환되고, 발신자 원본 포트 번호는 `공용 네트워크 인터페이스`의 TCP 포트 번호로 변환

3. 패킷이 인터넷을 통해 전송... 목적지인 대상 호스트 IP 주소에 도달.

4. 수신받은 호스트 IP 주소(서버)에서는 `NAT 라우터의 인터넷 주소`를 대상으로 하는 응답 패킷을 전송

5. `NAT 라우터`에 패킷이 도달. 인바운드 패킷이므로 바인딩된 변환 규칙이 적용. 대상 주소가 원래 발신자(클라이언트)의 IP 주소로 다시 변경

6. 패킷이 내부 네트워크에 연결된 인터페이스를 통해 클라이언트에 전달

## 참고

https://docs.microsoft.com/ko-kr/azure/rtos/netx-duo/netx-duo-nat/chapter1

## 용어

- 네트워크 토폴로지:
  - 토폴로지: 망 구성방식. 컴퓨터 네트워크 요소(노드, 링크 등)을 물리적으로 연결해 놓은 것.
  - 물리적 네트워크 토폴로지: 노드, 링크와 같은 네트워크를 구성하는 요소들의 배치에 의해 결정
  - 논리적 네트워크 토폴러지: 노드들 사이의 데이터 흐름에 의해 결정
  - 종류:
    - 버스
    - 스타
    - 링
    - 트리
    - 메시
      - 완전 메시형
      - 부분 메시형
