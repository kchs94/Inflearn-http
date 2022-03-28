# HTTP 웹 기본 지식

## 인터넷 통신

- IP(Internet Protocol, 인터넷 프로토콜)
  - 지정한 IP 주소(IP Address)에 데이터를 전달합니다.
  - 패킷(Packet)이라는 통신 단위로 데이터를 전달합니다.
- 패킷
  - 패킷에는 출발지IP, 목적지IP, 전송할 데이터 등이 들어있습니다.
- IP 프로토콜의 한계
  - 비연결성:패킷을 받을 대상이 없거나 서비스 불능 상태여도 패킷을 전송합니다.
  - 비신뢰성
    - 중간에 패킷이 사라질 수 있습니다.
    - 패킷이 순서대로 목적지에 도달하지 않을 수 잇습니다.
  - 프로그램 구분
    - 같은 IP를 사용하는 서버에서 통신하는 애플리케이션이 둘 이상이라면?


## TCP/ UDP

- 인터넷 프로토콜 스택의 4계층
- 애플리케이션 계층 - HTTP, FTP
- 전송 계층 - TCP, UDP
- 인터넷 계층 - IP
- 네트워크 인터페이스 계층


### TCP 특징

- 전송 제어 프로토콜(Transmission Control Protocol)
- 연결을 지향한다. - TCP 3 way handshake(가상 연결)
- 손실없는 데이터 전달을 보증한다.
- 순서를 보장한다.
- 신뢰할 수 있다.
- 현재 대부분 TCP를 사용한다.


### TCP 3 way handshake

1. SYN: 클라이언트에서 서버로 연결을 요청한다.
2. SYN+ACK: 서버는 앞서 들어온 요청을 수락한다. 클라이언트에게 연결을 요청한다.
3. ACK:클라이언트는 들어온 요청을 수락한다.
4. 데이터를 전송한다.

### 데이터 전달 보증

1. 클라이언트에서 서버로 데이터를 전송한다.
2. 서버는 클라이언트에서 보낸 데이터를 받고 받은 사실을 클라이언트에게 응답한다.


### 순서 보장

예를 들어서 설명한다.

1. 클라이언트에서 패킷1, 패킷2, 패킷3 순서로 전송한다.
2. 그런데 서버에 패킷1, `패킷3`, 패킷2 순서로 도착했다.
3. 서버는 클라이언트에게 패킷2부터 다시 보내라고 응답한다.


### UDP 특징

- 사용자 데이터그램 프로토(User Datagram Protocol)
- 하얀 도화지에 비유한다.(기능이 거의 없다)
- 연결을 지향한다 - TCP 3 way handshake X
- 손실없는 데이터 전달을 보증하지 않는다.
- 데이터가 순서대로 들어오는 것을 보장하지 않는다.
- 전달 및 순서를 보장하지는 않지만 전송 속도가 빠르다.
- 정리
  - IP와 거의 같다. PORT와 체크섬만 추가된 정도
  - 애플리케이션에서 추가 작업이 필요하다.


## PORT

- TCP 세그먼트에는 출발지 PORT, 목적지 PORT, 전송제어, 순서, 검증정보, 전송데이터가 포함된다.
- IP 패킷에는 출발지 IP, 도착지 IP, TCP 세그먼트로 구성된다.
- 즉 패킷에는 출발지 IP, PORT 정보와 도착지 IP, PORT 정보 + 전송데이터 등 이 있다.
- PORT는 같은 IP 안에서 프로세스를 구분한다.
- 0~65535까지 할당을 할 수 있다.
- 0~1023은 잘 알려진 포트다. 따라서 따로 사용하지 않는 것이 좋다.
  - FTP는 20,21 포트를 사용한다.
  - TELNET은 23포트를 사용한다.
  - HTTP는 80포트를 사용한다.
  - HTTPS는 443포트를 사용한다.


## DNS

- IP는 기억하기 어렵다
- IP는 변경될 수 있다.
- 도메인 네임 시스템(Domain Name System)
- 도메인 명을 IP 주소로 변환해준다.


### DNS을 사용하면?

1. 브라우저 검색창에 'www.google.com'을 입력한다.
2. DNS 서버는 요청으로 들어온 도메인 명('google.com')에 매칭되는 IP주소를 브라우저에게 응답한다.
3. 브라우저는 받은 IP주소로 구글 웹홈페이지를 응답받는다.


---

## URI

- 단일 자원 식별자(Uniform Resource Identifier)
- URL과 URN을 포함하는 개념이다.
  - URL(Resource Locator)
    - http://naver.com:8080/over/there?name=ferrt#nose
    - http 위치: 스키마
    - naver.com:8080 위치: authority
    - /over/there 위치: path
    - name=ferret 위치: query
    - noes 위치 fragment
  - URN(Resource Name)
    - urn:example:animal:ferret:nose
      - urn 위치: 스키마
      - example:animal:ferret:nose 위치: path

### URI 의미

- Uniform: 리소스를 식별하는 합의된 방식
- Resource: 자원, URI로 식별할 수 있는 모든 것. 
- Identifier: 다른 항목과 구분하는데 필요한 정보


### URL, URN 의미

- URL - Locator: 리소스가 있는 위치를 지정
- URN - Name: 리로스에 이름을 부여
- 위치는 변하지만 이름은 변하지 않는다.
- urn:isbn:892312312 (특정 책의 isbn URN)
- URN 이름만으로 리소스를 찾는 방법은 보편화되지 않았다.
- 앞으로 URI와 URL은 같은 의미로 취급한다.


### URL 구조

- schema://\[userinfo@]host\[:port]\[/path]\[?query][#fragment]
- https://<d>www.<d>google.com:443/search?q=hello&hl=ko
- 프로토콜은 https
- 호스트명은 www.<D>google.com
- 포트번호는 443
- 패스는 /search
- 쿼리파라미터는 q=hello&hl=ko


### URL - Schema

- `https`://www<d>.google.com:443/search?q=hello&hl=ko
- 프로토콜을 입력하는 위치
- 프로토콜은 통신하는 규칙을 말한다.
  - 예를 들어, HTTP, HTTPS, FTP 등이 있다.
- http는 80포트, https 443포트를 주로 사용한다.
- 포트는 생략할 수 있다.
- http에 보안 기능을 추가한 것이 https다.


### URL - userinfo

- 사용자정보를 입력하는 위치
- 거의 사용하지 않는다.


### URL - host

- https://**www<d>.google.com**:443/search?q=hello&hl=ko
- 호스트명이라고 한다.
- 도메인명 또는 IP 주소를 입력한다.


### URL - PORT

- https://<d>www.<d>google.com:**443**/search?q=hello&hl=ko
- 포토 번호가 들어가는 위치
- 일반적으로 생략한다
- 생략시 http는 80, https는 443을 사용한다.


### URL - path

- https://<d>www.<d>google.com:443**/search**?q=hello&hl=ko
- 리소스의 경로를 의미한다.
- 계층적인 구조다.
- 예시
  - /home/file1.jpg
  - /members/
  - /members/100, /items/iphone12


### URL - query

- https://<d>www.<d>google.com:443/search**?q=hello&hl=ko**
- 키:밸류 형태를 가진다.
- ?로 시작하고 &로 추가할 수 있다.
- 쿼리 파라미터, 쿼리 스트링으로 불린다.
- 웹서버에 제공하는 파라미터다.


### URL - fragment

- https://<d>docs.spring.io/spring-boot/docs/current/reference/html/getting-
  started.html**#getting-started-introducing-spring-boot**
- html 북마크 등에 사용된다.
- 서버에 전송하는 정보가 아니다.


## 웹브라우저 요청의 흐름

1. http://<d>www.<d>google.com:433/search?q=hello&hl=ko 엔터
2. DNS 서버에서 도메인명과 매칭되는 IP주소를 반환
3. HTTP 요청 메세지가 생성된다.
   - GET /search?q=hello&hl=ko HTTP/1.1
   - Host:www.<d>google.com
4. HTTP 요청 메세지를 서버에 전송한다.
   1. 소켓 라이브러리를 통해 브라우저(애플레케이션 계층)에서 TCP/IP로 이동한다.
   2. TCP/IP 패킷을 생성한다.패킷 안에 HTTP 요청 메세지가 들어있다.
   3. 네트워크 인터페이스 계층으로 이동하고 인터넷을 통해 서버로 전달된다.
5. 서버는 HTTP 응답 메세지를 브라우저(클라이언트)에 전송한다.
   - HTTP/1.1 200 OK
   - Content-Type: text/html;charset=UTF-8
   - Content-Length:3423
   - 공백
   - \<html>... 데이터 
6. 브라우저는 받은 html 데이터를 렌더링하여 화면에 출력한다.

---

# HTTP

목차
- HTTP로 모든 것을 전송할 수 있다.
- 클라이언트 서버 구조
- Stateful, Stateless
- 비 연결성(connectionless)
- HTTP 메세지


## HTTP로 모든 것을 전송할 수 있다.

- HTTP로 거의 모든 형식의 데이터를 전송할 수 있다.
- 텍스트, HTML
- 이미지, 음성, 영상, 파일
- JSON, XML (API)
- 서버간 데이터를 주고 받을 때도 HTTP을 사용한다.


### HTTP 역사

- HTTP/0.9: 91년, GET 메소드만 지원, HTTP 헤더 X
- HTTP/1.0: 96년, 메소드와 헤더가 추가되었다.
- **HTTP/1.1: 97년, 가장 많이 사용하는 버전, 우리에게 중요한 버전**
  - RFC2068(97년) -> RFC2616(99년) -> RFC7230~7235(14년)
- HTTP/2: 15년, 성능을 개선했다.
- HTTP/3: 진행중, TCP 대신 UDP를 사용한다. 성능을 개선했다.

### 기반 프로토콜

- TCP는 HTTP/1.1, HTTP/2를 사용한다.
- UDP는 HTTP/3을 사용한다.
- 현재는 HTTP/1.1을 주로 사용한다. 
- HTTP/2와 HTTP/3도 점점 증가하고 있다.


### HTTP 특징

- 클라이언트 서버 구조다.
- 무상태 프로토콜(스테이스리스)이다. 비연결성
- HTTP 메세지
- 단순하고 확장하기 쉽다.


### 클라이언트 서버 구조

- 요청과 응답 구조다.
- 클라이언트는 서버에 요청을 하고 응답을 대기한다.
- 서버가 요청에 대한 결과를 만들어서 응답한다.


### 무상태 프로토콜(스테이스리스)

- 서버가 클라이언트의 상태를 저장하지 않는다.
- 장점: 서버 확장성이 높다(스케일 아웃)
- 단점: 클라이언트가 추가 데이터를 전송해야 한다.


### Stateful, Stateless 차이

- 상태유지: 중간에 다른 점원(=서버)으로 바뀌면 안된다.
  - 서버에서 상태를 저장한다
  - 클라이언트A: 노트북, 2개
- 무상태: 중간에 다른 점원(서버)로 바뀌어도 된다.
  - 갑자기 고객이 증가해도 점원을 대거 투입할 수 있다.
  - 갑자기 클라이언트 요청이 증가해도 서버를 대거 투입할 수 있다.
  - 요청 HTTP 메세지에 클라이언트 상태를 넣어서 보낸다.
  - 요청 HTTP 메세지: 노트북, 2개
- 무상태는 응답 서버를 쉽게 바꿀 수 있다. 즉 서버를 쉽게 증설할 수 있다.
  - 스케일 아웃(=수평 확장), 즉 같은 기능을 하는 서버를 늘리기가 쉽다.


### 무상태 실무 한계

- 모든 것을 무상태로 할 수는 없다.
- 예를들어 로그인이 필요없는 단순 서비스 소개 화면은 무상태가 가능하다.
- 하지만 로그인의 경우는 상태 유지가 필요하다.
- 로그인한 사용자의 경우 로그인 했다는 상태를 서버에 유지해야 한다.
- 일반적으로 브라우저 쿠키와 서버 세션 등을 사용해서 상태를 유지한다.
- 상태 유지는 최소한으로 사용해야 한다.

## 비 연결성(Connectionless)

- TCP/IP로 연결되어 요청과 응답을 보낸다.
- 연걸을 유지하는 모델의 경우 서버는 클라이언트와 연결을 계속 유지하기 때문에 서버 자원을 많이 소모한다.
- 연결을 유지하지 않은 모델의 경우 서버는 클라이언트와 요청, 응답이 끝나면 연결을 끊는다. 따라서 자원 소모를 최소화 할 수 있다.
- HTTP는 기본적으로 연결을 유지하지 않는다.
- 일반적으로 초 단위 이하의 빠른 속도로 응답한다.
- 1시간 동안 수천명이 서비스를 사용해도 실제 서버에서 동시에 처리하는 요청은 거의 없다.
  - 웹브라우저에서 계속 연속해서 검색버튼을 누르는 사람은 없다.
- 서버 자원을 효율적으로 사용할 수 있다.

### 비연결성의 한계와 극복

- 비연결성을 지니다 보니 계속 TCP/IP 연결을 해야한다. 즉 3 way handshake 시간이 추가된다.
- 웹브라우저 사이트를 요청하면 html뿐만이 아니라 자바스크립트, css, 이미지 등 많은 자원이 다운로드 된다.
- 지금은 HTTP 지속 연결(Persistent Connections)로 문제를 해결한다.
- HTTP/2, HTTP/3에서 더 많은 최적화가 되고 있다.

### HTTP 초기 - 연결, 종료 낭비

네이버 홈페이지 보여줘

- 연결 0.1초
- 요청/HTML 응답 0.1초
- 종료
- 연결 0.1초
- 요청/자바스크립트 응답 0.1초
- 종료
- 연결 0.1초
- 요청/이미지 응답 0.1초
- 종료
- 합:0.9초


### HTTP 지속 연결(Persistent Connection)

네이버 홈페이지 보여줘
- 연결 0.1초
- 요청/HTML 응답 0.1초
- 요청/자바스크립트 응답 0.1초
- 요청/이미지 응답 0.1초
- 종료
- 합:0.5초


### 스테이스리스를 기억하자

- 서버개발자들 어려워하는 업무
- 정말 같은 시간에 딱 맞춰 발생하는 대용량 트래픽
- 예를들어 선착순 이벤트, 명절 KTX 예약, 학과 수업 등록
- 수만명이 동시 요청을 한다.


## HTTP 메세지


### HTTP 메세지 구조

- start-line: 시작라인
- header: 헤더
- empty line: 공백라인(CRLF)
- message body: 


### 요청 메세지 예시

- GET /search?q=hello&hl=ko HTTP/1.1 --> start-line
- Host:www.<d>google.com --> header
- .  --> 공백
- .  --> message-body (요청 메세지도 메세지 바디를 가질 수 있음)


### 응답 메세지 예시
- HTTP/1.0 200 OK --> start-line
- Content-Type: text/html;charset=UTF-8 --> header
- Content-Length: 3423 --> header
- . --> 공백 
- \<hmtl> ... --> message-body


### 요청 메세지 start-line(=request-line, status-line) 구조
- 예를들어 GET /search?q=hello&hl=ko HTTP/1.1
- HTTP 메소드 + 공백 + 요청대상 + 공백 + HTTP버전


### Http 요청 메세지의 시작라인 - HTTP 메소드

- 종류: GET, POST, PUT, PATCH, DELETE 등
- 서버가 해야할 행동을 지정합니다.
  - GET: 리소스 조회
  - POST: 요청 내역 처리

### HTTP 요청 메세지의 시작라인 - 요청 대상

- absolute-path\[?query](절대경로\[q쿼리])
- 절대경로란 '/'로 시작하는 경로를 말합니다.

### HTTP 응답 메세지의 시작라인(=status line) 구조

- HTTP버전 공백 상태코 공백 이유문구
- HTTP 상태 코드: 요청이 성공인지 실패인지를 나타낸다.
  - 200:성공
  - 400:클라이언트 요청 오류
  - 500:서버 내부 오류
- 이유 문구: 사람이 이해할 수있는 짧은 문구

### HTTP 메세지의 헤더

- Host:www.<d>google.com
- Content-Type:text/html;charset=UTF-8
- Content-Length: 3423
- 필드명:OWS field-value OWS  (OWS: 띄어쓰기 허용)
- 필드명은 대소문자를 구분하지 않는다.


### HTTP 메세지 헤더의 용도

- HTTP 전송에 필요한 부가정보가 들어있다.
- 메세지바디의 형식, 메세지바디의 크기, 압축, 인증, 요청클라이언(브라우저) 정보, 서버 애플리케이션 정보, 캐시관리 정보
- 표준 헤더가 정말 많다.
- 필요시 임의 헤더를 직접 만들어서 추가할 수 있다.
  - helloworld: hihi


### HTTP 메세지 message-body의 용도

- 실제 전송할 데이터를 담는다.
- HTML, 이미지, 영상, json 등 바이트로 표현할 수 있는 모든 데이터를 전송할 수 있다.

## HTTP 정리

- HTTP 메세지로 모든 종류의 데이터를 전송할 수 있다.
- HTTP/1.1을 기준으로 학습한다.
- 클라이언트 서버 구조를 가진다.
- HTTP는 무상태 프로토콜이다.
- HTTP 메세지
- 단순하고 확장하기 쉽다.


