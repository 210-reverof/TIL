# 트랜스포트 계층 서비스

## 트랜스포트 서비스와 프로토콜

- 서로 다른 호스트에서 동작하는 애플리케이션 스포세스 가느이 논리적 통신을 제공
- 트랜스포트 프로토콜은 종단 시스템에서 구현
    - 송신 : 애플리케이션 메시지를 세그먼트로 분할하여 네트워크 계층에 전달
    - 수신 : 세그먼트를 메시지로 결합하여 애플리케이션 계층에 전달
- 애플리케이션에 하나 이상의 트랜스포트 프로토콜
    - 인터넷 : TCP와 UDP

## 트랜스포트와 네트워크 계층

- 네트워크 게층 : 호스트들 사이의 논리적 통신을 제공
- 트랜스포트 계층 : 프로세스들 사이의 논리적 통신을 제공, 네트워크 계층 서비스에 의존

## 트랜스포트 계층 동작

### 송신

- 애플리케이션 계층에서 메시지 전달 받음
- 트랜스포트 계층의 헤더 필드 값 부가하여 세그먼트 생성
- IP 계층에 세그먼트 전달

### 수신

- IP 계층에서 메시지 전달 받음
- 헤더 값 조사
- 애플리케이션 계츠으이 메시지 추출
- 소켓을 통해 애플리케이션 계층으로 역다중화

## 인터넷 트랜스포트 프로토콜 계층

지연과 대역폭은 보장하지 못한다.

### TCP

- 신뢰적, 순서적인 데이터 전달
- 혼잡제어, 흐름제어, 연결 설정

### UDP

- 비순서적인 데이터 전달
- IP와 같은 최선형 전달 서비스 (best-effort delivery service)

# 다중화와 역다중화
- 다중화(multiplexing) : 캡슐화된 세그먼트들을 네트워크 계층으로 전달하는 작업
- 역다중화(demultiplexing) : 네트워크 계층을 통해 도착한 데이터를 트랜스포트 계층 세그먼트의 데이터를 올바른 소켓으로 전달하는 작업

## 역다중화 동작
- 호스트는 IP 데이터그램을 수신
    - 데이터그램은 출발지 IP 주소, 목적지 IP 주소를 가짐
    - 데이터그램은 한 개의 트랜스포트 계층 세그먼트를 가짐
    - 세그먼트는 출발지, 목적지 포트번호를 가짐
- 호스트는 IP 주소와 포트번호를 사용하여 세그먼트를 해당 소켓에 전달

### 비연결형 역다중화 (Connectionsless Demultiplexing)

- 포트번호를 갖는 소켓을 생성
- UDP 소켓으로 송신하는 데이터그램에는 목적지 IP 주소, 목적지 포트번호가 필수 포함
- 호스트가 UDP 세그먼트 수신 시
    - 세그먼트 내의 목적지 포트번호를 조사
    - 해당 포트번호를 갖는 소켓에 UDP 세그먼트를 전달
    - IP 데이터그램들의 출발지 IP 주소 또는 출발지 포트번호가 다르더라도 모두 동일한 목적지 IP 주소와 목적지 포트번호를 가지면 같은 소켓에 전달

### 연결지향형 역다중화 (Connection-Oriented Demultiplexing)

- TCP 소켓은 4개 요소로 구분 : 출발지 IP 주소, 출발지 포트번호, 목적지 IP주소, 목적지 포트번호
- 수신 측 호스트는 4개의 값 모두를 사용하여 해당 소켓으로 세그먼트 전달
- 서버 호스트는 동시에 많은 TCP 소켓들을 지원할 수 있음
    - 각 소켓들은 자신의 4개 요소로 구분
    - 각 소켓은 서로 다른 클라이언트 연결과 연관
