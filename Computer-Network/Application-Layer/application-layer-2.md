# REST

- 자원에 대한 명령은 CRUD로 압축 (Create, Read, Update, Delete)
- REST는 HTTP 메서드로 원격의 자원을 제어하는 명령을 기술 (POST, GET, PUT, DELETE)
- 명령의 결과 데이터는 HTTP 바디(body)로 전송 : XML, JSON etc

# 전자메일 (Electronic Mail, E-Mail)

- 3개의 주쇼 요소 : 사용자 에이전트, 메일 서버, SMTP (Simple Mail Transfer Protocol)

### 사용자 에이전트

- 메일 리더(mail reader)라고도 함
- 메시지를 읽고, 작성하고, 보내고, 전달
- MS outlook, Mozila Thunderbid 등
- 송수신 메시지는 서버에 저장

### 메일 서버 (main server)

- 받은 메시지를 유지하고 관리하는 메일박스 (mail box)
- 보내는 메시지의 메시지 큐 (message queue)
- 메일 서버들 간의 SMTP 프로토콜
    - 클라이언트 : 보내는 메일 서버
    - 서버 : 받는 메일 서버

### SMTP

- 클라이언트의 메일 메시지를 25번 포트의 TCP 연결 : 보내는 서버에서 받는 서버로 직접 전송
- 3단계 전송 과정 : SMTP 핸드세이킹 → SMTP 메시지 전송 → SMTP 종료
- HTTP와 같이 명령/응답 상호 작용
    - 명령(command) : ASCII 문자
    - 응답(response) : 상태 코드와 문장
- SMTP는 수신자의 서버에 E-mail 메시지를 전송하고 저장 → **메일 접속 프로토콜**이 서버로부터 메시지를 추출
    - IMAP(Internet Mail Access Protocol) : 서버에 저장된 메시지를 관리 : 조회, 삭제, 폴더 생성
    - HTTP : SMTP, IMAP의 위에서 웹 기반 인터페이스 제공

## SMTP 특징

- SMTP는 지속 연결을 사용
- SMTP 메시지(헤더 & 몸체)는 7-비트 ASCII로 표시
- SMTP 서버는 메시지의 끝을 CRLF.CRLF로 표시
- HTTP와 비교
    - HTTP :클라이언트 풀(pull) 프로토콜
    - SMTP : 클라이언트 푸시(push) 프로토콜
    - 모두 ASCII 명령/응답 상호 작용을 하고 응답 코드를 가짐
    - HTTP : 각 객체는 응답 메시지에 캡슐화
    - SMTP: 모든 메시지의 객체를 한 메시지로 만듬

# DNS (Domain Name System)

- 호스트 네임을 IP 주소 변환하는 디렉터리 서비스
- DNS 서버들이 계층구조로 구현된 분산 데이터베이스 (distributed database)
- 호스트가 분산 데이터베이스로 질의하여 호스트 네임에서 IP 주소를 획득하는 애플리케이션 계층 프로토콜

### DNS 서비스

- 호스트 네임을 IP 주소로 변환
- 호스트 에일리어싱 (host aliasing) : 간단한 별칭 호스트 네임을 복잡한 정식 호스트 네임
- 메일 서버 에일리어싱 (mail server aliasing)
- 부하 분산 (load distribution) : 여러 IP 주소들이 하나의 정식 호스트 네임과 연관되는 중복 웹 서버
- 단일 중앙 집중 방식 DNS를 사용하지 않는 이유 : 서버 고장 시 전체 작동하지 않음, 트래픽 양, 먼 거리의 중앙 집중 데이터베이스, 유진관리, 확장성 없음

### DNS 고려 사항

- 대규모 분산 데이터 베이스 : 수십억 개의 단순한 레코드
- 매일 수 조개의 질의 처리 : 쓰기보다는 읽기 위주, 성능이 중요
- 각 기관, 조직 별로 물리적으로 분산 : 수 백만개의 서로 다른 기관들이 레코드에 책임
- 신뢰성, 보안이 중요


### DNS 분산 계층 데이터베이스

- DNS 클라이언트가 [www.naver.com](http://www.naver.com) 호스트 네임의 IP 주소를 질의하는 과정
    - .com의 DNS 서버를 찾기 위해 루트(root) 서버에 질의
    - amazon.com의 DNS 서버 주소를 위해 .com의 DNS 서버(TLD 서버, top-level domain server)에 질의
    - [www.naver.com](http://www.naver.com) 의 IP 주소를 얻기 위해 naver.com의 DNS 서버 (책임 서버, authoritative server)에 질의

### DNS 루트 네임 서버

- 질의된 호스트 네임을 해결하지 못한 (IP 주소를 알지 못하는) 네임 서버들이 최종적으로 접촉
- ICANN (Internet Corporation for Assigned Names and Numbers) : 루트 네임 서버 관리

### TLD 서버 (Top-Level Domain Servers)

- .com, .org, .net, .edu 등과 같은 상위 레벨 도메인과 .kr, .uk, .fr, .jp 등과 같은 국가의 상위 레벨 도메인에 대해 책임
    - Network Solutions 사 : .com, .net
    - Educause : .edu
- 책임 DNS 서버 (Authoriatitve DNS servers)
    - 기관(회사, 대학 등)의 서버(웹 서버, 메일 서버 등)의 호스트 네임을 IP 주소로 매핑
    - 기관이나 서비스 제공자 등이 서버를 관리
- 로컬 DNS 네임 서버는 DNS 계층에 속하지 않음

### DNS 캐싱

- 네임 서버는 어떤 이름에 대해 받은 응답 정보를 캐싱하고 저장된 정보를 사용하여 질의에 즉시 응답
    - 캐싱으로 응답 시간이 개선
    - 캐싱된 정보는 일정 시간이 지나면 소멸
    - 일반적으로 로컬 네임 서버에 TLD 서버들이 캐싱 → 루트까지 갈 일 적음
- 캐싱된 정보가 최신 값이 아닐 수도 있음
    - 호스트의 IP 주소가 변경된 경우
    - 최선의 노력 방식으로 이름-주소 변환 시도!


### DNS 레코드

- DNS는 자원 레코드(resource record, RR)를 저장하는 분산 데이터베이스
> RR format : (name, value, type, ttl)
- type 4가지 정리
    - Type = A (host Address) : name은 호스트네임, valuse

|제목|내용|설명|
|------|---|---|
|테스트1|테스트2|테스트3|
|테스트1|테스트2|테스트3|
|테스트1|테스트2|테스트3|
