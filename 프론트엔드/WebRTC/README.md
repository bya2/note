# WebRTC

## 개요

- 웹에서 사용 가능한 유일한 `P2P`
- `UDP` 기반의 스트리밍 기술
- 웹 앱과 웹 사이트가 중간자 없이, 브라우저 간에 오디오나 영상 미디어를 포착하고 마음대로 스트림할 뿐 아니라 임의의 데이터도 교환할 수 있도록하는 기술.

- 브라우저와 단말 간 데이터를 주고 받는 `웹 표준` 기술
- `오픈 소스`

- 각각의 기기가 서버의 도움 없이 연결되기 위해, `Signaling`(연결을 도와주는 서버)이 필요
- P2P 연결이 불가능한 상황에 대처하기 위해, `TURN`(릴레이 서버)이 필요

- `P2P`, `UDP` 기반의 여러 프로토콜 덕에 WebRTC를 이용한 스트리밍은 현존하는 기술 중 Latency가 가장 짧음.

## 상호 운용성

각 브라우저마다 다른 코덱 및 기타 미디어 기능에 대한 지원 수준이 다름.
[Adapter.js](https://github.com/webrtcHacks/adapter) [설치 및 구성](./WebRTC-Adapter.md)

## 개념, 사용

- 피어들 간의 커넥션에는, 어떤 드라이버나 플러그인을 필요로 하지 않음 - `RTCPeerConnection` 인터페이스를 이용
- 커넥션이 이루어지고 열리면, `MediaStream(미디어 스트림)`들과 `RTCDataChannel(데이터 채널)`들을 커넥션에 연결 가능
  - `MediaStream`: 미디어 정보를 가지는 다수의 트랙(`MediaStreamTrack`)들로 구성
  - `MediaStreamTrack` 인터페이스 객체를 기반으로 하는 트랙은 음성, 영상, 텍스트를 포함하는 다양한 미디어 데이터 타입 중 하나를 포함 가능
  - 대부분의 스트림들은 한 개 이상의 트랙으로 구성되어 있고, Live 미디어나 저장된 미디어들을 송신/수신 가능
  - 임의의 바이너리 데이터를 `RTCDataChannel` 인터페이스를 통해 `Peer`들 간에 교환 가능

### 연결 및 설정 관리

- `RTCPeerConnection`: 로컬과 원격 Peer 간의 WebRTC 연결. (두 피어간 효율적인 데이터 스트리밍 처리에 이용)

  - `RTCIceCandidate`: `RTCPeerConnection` 설정을 위한 후보 `ICE` 서버
  - `RTCIceTransport`: `ICE` 전송에 대한 정보
  - `RTCPeerConnectionIceEvent`: `RTCPeerConnection`을 대상으로 한 `ICE` 후보와 관련하여 발생하는 이벤트 (`icecandidate`)

- `RTCDataChannel`: 두 Peer 간의 양방향 데이터 채널.

- `RTCDataChannelEvent`: `RTCDataChannel`을 `RTCPeerConnection`에 연결하는 동안 발생하는 이벤트.

- `datachannel`: `RTCDataChannelEvent`와 함께 전송되는 유일한 이벤트.

- `RTCSessionDescription`: 세션의 매개 변수. (세션의 설명자의 기술 제안/응답 협상 과정의 일부를 나타내는 설명)

- `RTCStatsReport`: 연결 또는 연결의 개별 트랙에 대한 통계를 자세히 설명하는 정보를 제공.

- `RTCRtpSender`: `RTCPeerConnection`에서 `MediaStreamTrack`의 데이터 인코딩 및 전송을 관리
- `RTCRtpReceiver`: `RTCPeerConnection`에서 `MediaStreamTrack`의 데이터 디코딩 및 수신을 관리

- `RTCTrackEvent`: 새롭게 수신된 `MediaStreamTrack`이 생성되고 관련 `RTCRtpReceiver` 개체가 `RTCPeerConnection` 개체에 추가되었음을 나타

## 용어

`P2P`: Peer To Peer
`Peer`: 단말, 장치, 브라우저
`UDP`: User Datagram Protocol` `바이너리 데이터`: 이미지든 텍스트든 파일이든 모두 가능하다는 뜻 `ICE`: 인터넷 연결 설정
