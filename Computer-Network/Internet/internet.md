# 인터넷

## 구성 요소 관점

- 장치 (device)
    - 호스트(host) = 종단 시스템 (end system)
    - 가장자리(edge)에서 네트워크 응용들을 수행
- 패킷 스위치 (packet switch)
    - 패킷(데이터의 덩어리)을 전달 : forward
    - 라우터(router), 스위치(switch)
- 통신 링크 (communication link)
    - 광섬유, 동축케이블, 전파 위성
    - 다양한 전송 속도(transmission rate 또는 bandwidth)로 데이터(패킷) 전송
- 네트워크 (networks)
    - 장치, 라우터, 링크들의 집합
    - 기관 및 조직에서 관리
- 인터넷(Internet)
- 프로토콜(protocol)
    - 정보(메시지)의 송수신을 제어
    - HTTP(웹), 스트리밍 비디오, TCP, IP, WiFi, 4G/5G, Ethernet
- 인터넷 표준 (Internet standards)
    - IETF (Internet Engineering Task Force)
    - RFC (Request For Comments) : IETF 표준문서

## 서비스 관점

- 애플리케이션에 서비스를 제공하는 인프라구조(infrastucture)
    - 웹, 스트리밍 비디오, 화상회의, 이메일, 게임, 전자상거래
    - 부산된 애플리케이션에 프로그래밍 인터페이스 제공
        - 인터넷에 접속하여 송수신 응용들에게 연결되고, 인터넷 전송 서비스(TCP)를 사용
        - 우편 서비스와 유사한 서비스 제공

## 프로토콜 (protocol)

- 사람 프로토콜 (human protocol)
    - 사람이 전달하고자 하는 특정 메시지
    - 수신 된 응답 메시지나 다른 상황에 반응하는 특정 행동
- 네트워크 프로토콜
    - 사람 대신 기계 장치들
    - 인터넷 상의 모든 활동은 프로토콜이 제어
    - 정의 : 프로토콜은 통신 개체들 간에 교환되는 메시지 형식(format)과 순서 뿐 아니라, 메시지의 송수신과 다른 이벤트에서 취하는 행동(동작)들을 정의

# 인터넷 구성 요소

- 네트워크 가장자리(edge)
    - 호스트 : 클라이언트와 서버
    - 데이터 센터 내의 서버들
- 접속 네트워크(access network), 물리 매체(physical media)
    - 유무선 통신 링크
- 네트워크 코어(core)
    - 상호 연결된 라우터
    - 네트워크들의 네트워크

## 네트워크의 가장자리

### 접속 네트워크와 물리 매체

- 종단 시스템과 가장자리 라우터(edge router) 접속
- 접속 네트워크 종류
    - 가정 접속 (residential access)
    - 기관 접속 (school, company access)
    - 무선 접속 (WiFi, 4G/5G)
    - DSL (Digital subscriber Line)
        - 지역 전화국의 DSLAM(DSL access multiplexer)까지는 기존의 전화선 사용
    - 케이블 네트워크
        - 주파수 분할 다중화 (frequency division multiplexing) : 각 채널들이 서로 다른 주파수 밴드로 전송
        - HFC (Hybrid Fiber Coax) 접속망
        - 케이블과 광섬유 네트워크가 각 가정을 ISP 라우터에 연결

### 무선 접속 네트워크 (Wireless Access Network)

- 공유 무선 접속 네트워크가 종단 시스템을 라우터에 연결
- 무선 LAN (wireless LAN) : ex. wifi
- 광역 무선 접속 (wider-area wireless access) : ex.4G/5G

### 링크 : 물리 매체 (Physical Media)

- 비트 (bit) : 송신기(transmitter)와 수신기(receiver) 사이에 전달
- 물리 링크 (physical link) : 송신기와 수시기 사이를 연결
- 유도 매체 (guided media) : 견고한 매체를 따라 신호 유도
    - **꼬임쌍선 (Twisted Pair, TP)** : 두 개의 절연 동선, UTP
    - **동축 케이블 (coaxial ccable)** : 동심원 형태의 두 개의 구리선, 브로드밴드
    - **광섬유 (Fiber Optics) :** 비트를 나타내는 빛의 파동을 전파, 낮은 에러율
- 비유도 매체 (unguided media) : 무선 통신의 경우처럼 야외 공간으로 파형을 자유롭게 전파
    - 무선 전자기 스펙트럼으로 신호를 전달 : 전파 환경 효과

## 네트워크 코어 (Network Core)

- 네트워크 코어는 상호 연결된 라우터들의 연결망 (mesh)
- 패킷 스위칭 (packet switching)
    - 호스트는 애플리케이션 계층의 메시지를 패킷(packet)이라 알려진 작은 덩어리로 분할
    - 패킷들은 송신 측과 수신 측의 경로 상의 링크와 라우터를 거쳐 전송
        - 패킷들은 한 라우터에서 다른 라우터로 전달(forward)
- 2가지 주요 기능
    - **포워딩 (forwarding)** : 스위칭이라고도 함. 라우터의 입력에서 적절한 라우터 출력으로 패킷을 이동
    - **라우팅 (routing)** : 소스에서 목적지까지의 패킷 경로를 결정

### 호스트의 패킷 전송

- 호스트의 송신 동작
    - 애플리케이션의 메시지를 받음
    - 메시지를 길이 L비트의 더 작은 덩어리인 패킷으로 분할
    - 패킷을 네트워크 전송률/전송속도 R로 전송
        - 링크 전송 속도는 용량 (capacity), 대역폭(bandwidth)라고도 함
        

### 패킷 스위칭 : 저장 후 전달 (store-and-forward transmission)

- L비트의 패킷을 R bps 속도의 링크로 전송하는데 L/R초 걸림
- 저장 후 전달 (store-and-forward transmission) : 다음 링크로 전송하기 전에 패킷 전부가 라우터에 도착해야 함
- 위 그림 지연 = 2L/R (전파 지연(propagation delay) 무시)

### 패킷 스위칭 : 큐잉 (Queuing)

- 입력 링크에 비트가 도착하는 속도가 내보내는 전송 속도보다 빠른 경우 큐잉 발생
- 패킷 큐잉과 손실 : 일정 시간 동안 라우터의 입력 링크에 비트가 도착하는 속도가 전송률보다 빠른 경우. 큐의 메모리가 꽉 차 있는 경우 패킷은 손실 됨

### 회선 교환 (Circuit Switching)

- 네트워크 코어 구성 방식은 회선 교환과 패킷 스위칭 두 가지 방식이 있음
- 회선 교환 (circuit switching)
    - 경로 상에 필요한 자원(버퍼, 링크 전송률)이 통신 세션 동안 예약
    - 자원이 공유되지 않음
    - 송신자와 수신자 간의 경로에 있는 스위피들이 연결 상태를 유지
    - 송신자와 수신자 간의 전송률 보장
    - 기존의 전화망
- 회선 교환에서 한 링크는 n개의 회선(circuit)을 연결
    - 네트워크 자원을 분할(다중화)
    - 자신의 호가 사용되지 않으면 분할된 자원은 쉼
