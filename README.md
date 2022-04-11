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

- https<d>://www<d>.google.com:**443**/search?q=hello&hl=ko
- 포토 번호가 들어가는 위치
- 일반적으로 생략한다
- 생략시 http는 80, https는 443을 사용한다.

### URL - path

- https<d>://www<d>.google.com:443**/search**?q=hello&hl=ko
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


---

# HTTP 요청 메소드

목차
- HTTP API를 만들어보자
- HTTP 메소드 - GET, POST
- HTTP 메소드 - PUT, PATCH, DELETE
- HTTP 메소드 속성


## HTTP API를 만들어 보자

### 요구사항: 회원 정보를 관리하는 API를 만들어라

- 회원 목록 조회
- 회원 조회
- 회원 등록
- 회원 수정
- 회원 삭제


### API URI 동사(행위)를 포함하여 설계하기

- 회원 목록 조회
  - /**read**-member-list
- 회원 조회
  - /**read**-member-by-id
- 회원 등록
  - /**create**-member
- 회원 수정
  - /**update**-member
- 회원 삭제
  - /**remove**-member


### 동사를 포함하는 URI는 좋은 URI가 아니다.

- 왜냐하면 좋은 URI 설계는 **리소스**(회원)를 식별(구별)한다.
- 위의 URI는 리소스가 아닌 **행위**를 식별(구분)한다.


### 좋은 API URI는 무엇일까?

- 좋은 URI는 리소스**만** 구별한다.
- 행위는 구별하지 않는다.
- 리소스는 명사고 행위는 동사다.
- 행위는 HTTP 메소드를 통해서 구별한다.


### 좋은 설계로 만든 회원 정보를 관리하는 API

- 회원 목록 조회
  - /members
- 회원 조회
  - /members/{id}
- 회원 등록
  - /members/{id}
- 회원 수정
  - /members/{id}
- 회원 삭제
  - /members/{id}

위와같이 URI를 설계하고 HTTP 메소드를 사용하여 행위를 구별한다.


## HTTP 요청 메소드 - GET, POST

### HTTP 요청 메소드 종류

주요 메소드
- GET: 리소스를 조회할 때 사용한다.
- POST: 요청 데이터를 처리할 때 사용한다. 주로 등록할 때 사용한다.
- PUT: 리소스를 대체한다. 리소스가 없으면 생성한다.
- PATCH: 리소스를 부분 변경한다.
- DELETE: 리소스슬 삭제한다.

기타 메소드
- HEAD: GET과 동일하지만 상태 줄과 헤더만 반환한다.
- OPTIONS: 대상 리소스에 대한 통신 가능 옵션(메소드)을 설명한다. (주로 CORS에서 사용한다.)
- CONNECT: 대상 자원으로 식별되는 서버에 대한 터널을 설정한다.
- TRACE: 대상 리소스에 대한 경로를 따라 메세지 루프백 테스트를 수행한다.

### GET 메소드

> GET /search?q=hello&hl=ko HTTP/1.1  
> Host:www<d>.google.com

- 리소스를 조회할 때 사용합니다.
- 서버에 전달하고 싶은 데이터가 있으면 쿼리파라미터(쿼리스트링)을 통해 전달합니다.
- 메시지 바디를 거의 사용하지 않습니다.

### GET 메소드 예시

#### 1.GET 요청 메세지 전송

> GET /members/100 HTTP/1.1  
> Host: localhost:8080

#### 2.서버에 있는 리소스 상태

- /members/100
> {  
>   "username": "young",  
>   "age": 20  
> }

#### 3.응답 메세지

> HTTP/1.1 200 OK  
> Content-Type: application/json  
> Content-Length: 34  
>   
> {  
>  "username": "young",  
>   "age": 20  
> } 


### POST 메소드

> POST /members HTTP/1.1  
> Content-Type: application/json  
>   
> {  
>   "username": "hello",  
>   "age": 20  
> }

- 메세지 바디에 있는 데이터의 **처리**를 요청합니다.
- 메세지 바디를 통해서 데이터를 전달합니다.
- 서버는 요청 데이터를 **처리**합니다.
- 일반적으로 전달된 데이터로 새로운 리소스를 등록하거나, 프로세스 처리에 사용합니다.

### POST 메소드 예시(리소스 등록)

#### 1.POST 요청 메세지 전송

> POST /members HTTP/1.1  
> Content-Type: application/json  
>   
> {  
>   "username": "young",  
>   "age": 22  
> }


#### 2.신규 리소스를 생성

- /members --> /members/100 신규 리소스 식별자(URI) 생성합니다.

> {  
>   "username": "young",  
>   "age": 22  
> }


#### 3.응답 메세지 전송

> HTTP/1.1 201 Created  
> Content-Type: application/json  
> Content-Length: 34  
> Location: /members/100  
>   
> {  
>   "username": "young",  
>   "age": 22  
> }


### 그런데 정확하게 처리한다는게 무슨 의미일까?

- HTML 양식에 입력된 데이터를 데이터 처리 프로세스에 제공합니다.
  - 예들들어 HTML Form에 입력한 정보를 회원가입, 주문 등에 사용합니다.
- 게시판, 블로그 등 기사 그룹에 메세지를 게시합니다.
  - 예를들어, 게시판 글쓰기, 댓글 달기
- 서버가 아직 식별하지 않은 새로운 리소스를 생성합니다.
  - 예를들어, 신규 주문을 생성합니다.
- 기존 자원에 데이터를 추가합니다.
  - 예를들어, 한 문서 끝에 내용을 추가합니다.
- 정리: 이 리소스 URI에 POST 요청이 오면 요청 데이터를 어떻게 처리할지 리소스마다 따로 정해줘야 합니다.즉 정해진 것이 없습니다.

### POST 정리

- 새로운 리소스를 등록(생성)할 때 사용합니다.
  - 서버가 아직 식별하지 않은 새로운 리소스
- 요청 데이터를 처리할 때 사용합니다.
  - 단순히 데이터를 생성하거나 변경을 넘어선 프로세스를 처리해야 하는 경우
  - 예를들면, 주문에서 결제완료 -> 배달시작 -> 배달완료처럼 단순히 값 변경 넘어 프로세스 상태가 변경되는 경우
  - POST의 결과로 리소스가 생성되지 않을 수도 있다.
  - 예를들어 POST /orders/{orderId}/start-delivery(**컨트롤 URI**)
- 다른 메소드로 처리하기 애매한 경우
  - 예를들면, JSON으로 조회 데이터를 넘겨야 되는데, GET 메소드를 사용하기 어려운 경우
  - 애매하면 POST 메소드를 사용합니다.


## HTTP 요청 메소드 - PUT, PATCH, DELETE

### PUT 메소드

> PUT /members/100 HTTP/1.1  
> Content-Type: application/json  
>   
> {  
>   "username": "hello",  
>   "age": 22  
> }

- 리소스를 대체할 때 사용합니다.
  - 리소스가 서버에 있으면 대체하고 없으면 생성합니다.
  - 쉽게 생각하면 덮어쓰기와 같습니다.
  - 리소스를 완전히 대체하기 때문에 필드가 삭제될 수 있습니다.
- 클라이언트가 리소스를 식별합니다.
  - 클라이언트가 리소스의 위치를 알고 URI를 지정합니다.
  - 이러한 점이 POST 메소드와의 차이점입니다.


### PUT 메소드 예시1 - 리소스가 있는 경우

#### 1.요청 메세지 전송하기 전 서버 

> PUT /members/100 HTTP/1.1  
> Content-Type: application/json  
>   
> {  
>   "username": "old",  
>   "age": 50  
> }

- 전송 전 서버 
- /members/100
> {  
>   "username": "young",  
>   "age": 20  
> }


#### 2.요청 메세지 전송 후 서버 

- 전송 후 서버
- /members/100
> {  
>   "username": "old",  
>   "age": 50  
> }

### PUT 메소드 예시2 - 리소스가 없는 경우

#### 1.요청 메세지 전송하기 전 서버

> PUT /members/100 HTTP/1.1  
> Content-Type: application/json
>
> {  
>   "username": "old",  
>   "age": 50  
> }

- 전송 전 서버
- /members/100는 없는 상태

#### 2.요청 메세지 전송 후 서버

- 전송 후 서버
- /members/100 신규 리소스 생성
> {  
>   "username": "old",  
>   "age": 50  
> }


### PATCH 메소드

> PATCH /members/100 HTTP/1.1  
> Content-Type: application/json  
>   
> {  
>   "age": 50  
> }

- 리소스를 부분적으로 변경합니다.

### PATCH 메소드 사용 예시 - 리소스 부분 변경

#### 1.요청 메소드 보내기 전 서버 상태

> PATCH /members/100 HTTP/1.1  
> Content-Type: application/json
>
> {  
>   "age": 50  
> }

- username 필드가 메세지 바디에 없습니다.
- 서버 상태
- /members/100

> {  
>   "username": "young",  
>   "age": 20  
> }

#### 2.요청 메소드 보낸 후 서버 상태

- 리소스 부분 변경
- /members/100
- age만 50으로 변경

> {  
>   "username": "young",  
>   "age": 50  
> }


### DELETE 메소드

> DELETE /members/100 HTTP/1.1  
> Host: localhost:8080

- 리소스를 제거하는 메소드입니다.

### DELETE 메소드 사용 예시 - 리소스 제거하기

#### 1.요청 메소드를 보내기 전 서버 상태

> DELETE /members/100 HTTP/1.1  
> Host: localhost:8080

- 서버 상태
- /members/100

> {  
>   "username": "young",  
>   "age": 50  
> }

#### 2.요청 메소드를 보낸 후 서버 상태

- 리소스 제거
- /members/100 (x)


## HTTP 메소드의 속성

- 안전(Safe Methods)
- 멱등(Idempotent Methods)
- 캐시가능(Cacheable Methods)

### 안전한 속성

- 메소드를 호출해도 리소스가 변경되지 않는다.
- 예를들어, GET,HEAD 등

### 멱등한 속성

- f(f(x)) = f(x)
- 한 번 호출하든 여러 번 호출하든 결과가 같다.
- GET: 한 번 조회하든, 여러 번 조회하든 같은 결과가 조회된다.
- PUT: 결과를 대체한다. 따라서 여러번 요청해도 최종 결과는 같다.
- DELETE: 결과를 삭제한다. 같은 요청을 여러번 해도 삭제된 결과는 같다.
- **POST**는 멱등이 아니다! 두 번 호출하면 같은 결제가 중복해서 발생할 수 있다.
- 활용
  - 자동 복구 메커니즘
  - 서버가 타임아웃 등으로 정상 응답을 주지 못할 때, 클라이언트가 같은 요청을 다시 해도 되는가? 판단 근거
- Q: 재요청 중간에 다른 곳에서 리소스를 변경해버리면?
  - 사용자1: GET-> username:A, age:20
  - 사용자2: PUT-> username:A, age:30
  - 사용자3: GET-> username:A, age:30 -> 사용자2의 영향으로 바뀐 데이터를 조회
- A:멱등은 외부 요인으로 중간이 리소스가 변경되는 것까지는 고려하지 않는다.

### 캐시가능한 속성(Cacheable)

- 응답 결과 리소스를 캐시해서 사용해도 되는가?
- GET, HEAD, POST, PATCH는 사용할 수 있다.
- 실제로드 GET, HEAD 정도만 캐시로 사용한다.
  - POST, PATCH로 본문 내용까지 캐시 키로 고려해야 되는데, 구현이 쉽지 않다.

--- 

# HTTP 메소드 활용하기

목차
- 클라이언트에서 서버로 데이터 전송하기
- HTTP API 설계 예시


## 클라이언트에서 서버로 데이터 전송하는 2가지 방법

### 쿼리 파리미터를 통한 데이터 전송하기

- GET 메소드를 사용한다
- 주로 검색과 같은 정렬 필터를 사용할 때 사용하는 방법이다.


### 메세지 바디를 통한 데이터 전송하기

- POST, PUT, PATCH 메소드를 사용한다.
- 회원 가입, 상품 주문, 리소스 등록, 리소스 변경등을 할 때 사용하는 방법이다.


### 클라이언트에서 서버로 데이터를 전송하는 4가지 상황

- 정적 데이터(텍스트, 이미지)를 조회 할 때
- 동적 데이터를 조회할 때
  - 주로 검색이나 게시판 목록에서 정렬 필터(검색어)를 사용할 때
- HTML Form을 통해서 데이터를 전송 할 때
  - 회원가입, 상품 주문, 데이터 변경 등
- HTTP API를 통해서 데이터를 전송할 때
  - 회원가입, 상품 주문, 데이터 변경 등
  - 서버 to 서버, 앱 클라이언트, 웹 클라이언트(Ajax)


### 정적 데이터를 조회할 때

- 쿼리 파라미터를 사용하지 않는다.
- 이미지, 정적 텍스트를 문서를 조회할 때에 해당한다.
- 조회할 때에는 GET 메소드를 사용한다.
- 정적 데이터는 쿼리파라미터없이 리소스 경로로 단순하게 조회할 수 있다.

> GET /static/star.jpg HTTP/1.1  
> Host: localhost:8080  

- /static/star.jpg
> HTTP/1.1 200 OK  
> Content-Type: image/jpeg  
> Content-Length: 34012  
>  .  
>  falf2l3j42ljrdlajff2lfj23ffadslfa  
>  f2l3fj23lfj23lkfj2lfj


### 동적 데이터를 조회할 때

> https:/<d>/www<d>.google.com/search?q=hello&hl=ko  

> GET /search?q=hello&hl=ko HTTP/1.1  
> Host: www.google.com  

- 쿼리 파라미터를 기반으로 필터링하여 데이터를 동적으로 생성한다.
- 조회이므로 GET 메소드를 사용한다.
- GET 메소드인데 데이터를 전송해야 할 경우에는 쿼리파라미터를 사용한다.


### HTML Form을 통한 데이터 전송

#### POST 전송을 통한 **저장**하기

``` html
<form action="/save" method="post"> 
  <input type="text" name="username" /> // kim 입력
  <input type="text" name="age" />  // 20 입력
  <button type="submit">전송</button>
</form>
```

- 요청 메세지
> POST /save HTTP/1.1  
> Host: localhost:8080  
> Content-Type: application/x-www-form-urlencoded  
>   . 
> username=kim&age=20


#### GET 전송을 통한 **저장**하기

``` html
<form action="/save" method="get"> 
  <input type="text" name="username" /> // kim 입력
  <input type="text" name="age" />  // 20 입력
  <button type="submit">전송</button>
</form>
```

- 요청 메세지 --> 잘못된 방식, GET은 조회할 때만 사용한다, 리소스 변경이 발생하는 곳(save)에서 사용하면 안됨.
> GET /save?username=kim&age=20 HTTP/1.1  
> Host: localhost:8080  



#### GET 전송을 통한 **조회**하기

``` html
<form action="/members" method="get"> 
  <input type="text" name="username" /> // kim 입력
  <input type="text" name="age" />  // 20 입력
  <button type="submit">전송</button>
</form>
```


> GET /members?username=kim&age=20 HTTP/1.1  
> Host: localhost:8080

#### multipart/form-data

```html
<form action="/save" method="post" enctype="multipart/form-data">
  <input type="text" name="username"/>
  <input type="text" name="age"/>
  <input type="file" name="file1"/>
  <button type="submit">전송</button>
</form>
```

- 요청 HTTP 메세지
> POST /save HTTP/1.1  
> Host: localhost:8080  
> Content-Type: multipart/form-data; boundary=-----XXX  
> Content-Length: 10457  
>   
> 
> -----XXX  
> Content-Disposition: form-data;name="username"  
> 
> 
> kim  
> -----XXX  
> Content-Disposition: form-data;name="age"  
>   
> 20  
> -----XXX  
> Content-Disposition: form-data;name="file1";filename="intro.png"  
> Content-Type: image/png  
>   
> 012998daskjfhaskf3hfakfjhakj  
> -----XXX--  
> 


### HTML Form을 통한 데이터 전송 요약

- HTML Form submit시 Post 메소드를 사용한다.
  - 예) 회원가입, 상품주문, 데이터 변경
- Content-Type: application/x-www-form-urlencoded 사용
  - form 내용을 메세지 바디를 통해서 전송한다.(key-value(=쿼리파라미터형식))
  - 전송 데이터를 url encoding 처리한다.
    - 예)abc --> abc%EA%B9%80
- HTML Form은 GET 전송도 가능하다.
- Content-Type: multipart/form-data
  - 파일 업로드 같은 바이너리 데이터 전송시 사용한다.
  - 다른 종류의 여러 파일과 폼의 내용 함께 전송 가능하다.
- HTML Form은 GET과 POST만 지원한다.


### HTTP API를 통한 데이터 전송

> POST /members HTTP/1.1  
> Content-Type: application/json
>   
> {  
>   "username": "young"  
>   "age": 20  
> }  

- 서버 to 서버 
  - 백엔드 시스템 통신
- 앱 클라이언트 
  - 아이폰, 안드로이드
- 웹 클라이언트
  - HTML에서 Form 전송 대신 자바스크립트를 통한 통신에 사용(AJAX)
  - 예)React, VueJS 같은 웹 클라이언트와 API 통신
- POST, PUT, PATCH: 메세지 바디를 통한 데이터 전송
- GET:조회, 쿼리 파라미로 데이터를 전송
- Content-Type:application/josn 주로 사용 (사실상 표준)
  - TEXT, XML, JSON 등 



## HTTP API 설계 예시

- HTTP API - 컬렉션
  - POST 기반으로 등록한다.
  - 예) 회원관리 API 제공
- HTTP API - 스토어
  - PUT 기반으로 등록한다.
  - 예) 정적 컨텐츠 관리, 원격 파일 관리
- HTML FORM 사용
  - 웹 페이지 회원 관리
  - GET, POST만 지원한다.

### 회원 관리 시스템 API 설계 - POST 기반 등록 

- 회원 목록 /members -> GET
- 회원 등록 /members -> POST
- 회원 조회 /members/{id} --> GET
- 회원 수정 /members/{id} --? PATCH, PUT, POST
- 회원 삭제 /members/{id} --? DELETE

### 회원 관리 시스템 POST 기반 신규 자원 등록 특징
- 클라이언트는 등록될 리소스의 URI를 모른다.
  - 따라서 회원등록은 POST /members
- 서버가 새로 등록된 리소스 URI를 생성한다.
  - HTTP/1.1 201 Created
  - Location: /members/100
- 컬렉션(Collection)
  - 서버가 관리하는 리소스 디렉토리를 말한다.
  - 서버가 리소스의 URI를 생성하고 관리한다.
  - 여기서 컬렉션은 /members


### 파일 관리 시스템 API 설계 - PUT 기반 등록 

- 파일 목록 /files --> GET
- 파일 조회 /files/{filename} --> GET
- 파일 등록 /files/{filename} --> PUT
- 파일 삭제 /files/{filename} --> DELETE
- 파일 대량 등 /files --> POST

### 파일 관리 시스템 API 설계 - 신규 자원 등록 특징

- 클라이언트가 리소스 URI를 알고 있다.
  - 파일 등록 /files/{filename} --> PUT
  - PUT /files/star.jpg
- 클라이언트가 직접 리소스의 URI를 지정한다.
- 스토어(Store)
  - 클라이언트가 관리하는 리소스 저장소를 말한다.
  - 클라이언트가 리소스의 URI를 알고관리한다.
  - 여기서 스토어는 /files


### HTML Form 사용

- HTML Form은 GET, POST만 지원한다.
- AJAX와 같은 기술을 사용해서 해결이 가능하 --> 회원 API 참고
- 여기서는 순수 HTML, HTML Form 이야기
- GET, POST만 지원하므로 제약이 있다.

### HTML Form 사용

- 회윈 목록 /members --> GET
- 회원 등록 폼 /members/new --> GET
- 회원 등록 /members/new, /members --> POST
- 회원 조회 /members/{id} --> GET
- 회원 수정 폼 /members/{id}/edit --> GET
- 회원 수정 /members/{id}/edit, /members/{id}--> POST
- 회원 삭제 /members/{id}/delete --> POST

- HTML Form은 GET,POST만 지원해서 제약이 생긴다
- 컨트롤 URI로 설계한다
  - GET,POST만 지원하므로 제약이 있으니깐
  - 이런 제약을 해결하기 위해 동사로된 리소스 경로를 사용할 수 밖에 없다.
  - POST의 /new, /edit/, /delete가 컨트롤 URI을 의미한다.
  - HTTP 메소드로 해결하기 애매한 경우에 사용한다.


### 정리

- HTTP API - 컬렉션
  - POST기반 등록
  - 서버가 리소스 URI를 결정한다.
- HTTP API - 스토어
  - PUT 기반 등록
  - 클라이언트가 리소스 URI를 결정한다.
- HTML FORM 사용
  - 순수 HTML + HTML Form 사용
  - GET, POST만 지원한다.

### 참고하면 좋은 URI 설계 개념

- 문서(document)
  - 단일 개념(파일 하나, 객체 인스턴스, 데이터베이스)
  - 예) /members/100, /files/star.jpg
- 컬렉션(collection)
  - 서버가 관리하는 리소스 디렉토리
    - 서버가 리소스의 URI를 생성하고 관리한다.
    - 예) /members
- 스토어(store)
  - 클라이언트가 관리하는 자원 저장소
  - 클라이언트가 리소스의 URI를 알고 관리한다
  - 예) /files
- 컨트롤(controller), 컨트롤 URI
  - 문서, 컬렉션, 스토어 해결하기 어려운 추가 프로세스 실행
  - 동사를 직접 사용한다.
  - 예) /members/{id}/delete


---

# HTTP 상태코드

> 클라이언트가 보낸 요청의 처리 상태를 숫자로 보여주는 기능

- 1xx(Informational): 요청이 수신되어 처리중을 나타냄
- 2xx(Successful): 요정이 정상적으로 처리됨
- 3xx(Redirection): 요청을 완료하려면 추가 행동이 필요함을 나타냄
- 4xx(Client Error): 클라이언트 오류(문법)으로 인해 서버가 요청을 수행할 수 없음
- 5xx(Server Error): 서버 오류로 인해 서버가 정상 요청을 처리하지 못함


### 만약 서버에서 클라이언트가 모르는 상태코드가 온다면?

- 클라이언트는 상위 상태코드를 찾아서 해석한다.
- 미래에 새로운 상태코드가 추가되어도 클라이언트를 변경하지 않아도 된다.
- 예
  - 299 ??? -> 2xx(성공)
  - 451 ??? -> 4xx(클라이언트 에러)
  - 599 ??? -> 5xx(서버 에러)

### 1xx(Informational)

- 요청이 수신되어 서버에서 처리중을 의미
- 거의 사용되지 않음


### 2xx(Successful)

- 클라이언트의 요청이 성공적으로 처리됨
- 200 OK
- 201 Created
- 202 Accepted
- 204 No Content


#### 200 OK

- 요청 성공

http 요청
> GET /members/100 HTTP/1.1  
> Host: localhost:8080  

http 응답
> HTTP/1.1 200 OK  
> Content-Type: application/json  
> Content-Length:34  
>   
> {  
>   "username": "young"  
>   "age": 20  
> }


#### 201 Created

- 요청에 성공해서 새로운 리소스가 생성됨

http 요청
> POST /members HTTP/1.1  
> Content-Type: application/json  
>   
> {  
>   "username": "young"  
>   "age": 20  
> }

http 응답
- 생성된 리소스는 응답의 Location 헤더 필드로 식별
> HTTP/1.1 201 Created  
> Content-Type: application/json  
> Content-Length: 34  
> Location: /members/100
>   
> {  
>   "username": "young"  
>   "age": 20  
> }

#### 202 Accepted

- 요청이 접수되었지만 아직 처리가 완료되지 않음
- 배치처리 같은 곳에서 사용됨
  - 예) 요청 접수 후 1시간 뒤에 배치 프로세스가 요청을 처리함


#### 204 No Content

- 서버가 요청을 성공했지만, 응답 페이로드 본문 보낼 데이터가 없는 상황
- 예) 웹 문서 편집기 save 버튼
- save 버튼의 결과로 아무 내용이 없어도 된다.
- save 버튼을 눌러도 같은 화면을 유지해야 한다.
- 결과 내용이 없어도 204 메시지 만으로 성공을 인식할 수 있다.


### 3xx(리다이렉션)

- 요청을 완료하기 위해 유저 에이전트의 추가적인 조치가 필요함을 나타냄
- 300 Multiple Choice
- 301 Moved Permanently
- 302 Found
- 303 See Other
- 304 Not Modified
- 307 Temporary Redirect
- 308 Permanent Redirect

### 리다이렉션의 이해

- 웹 브라우저는 3xx 응답 결과에 Location 헤더가 있으면, Location 위치로 자동 이동(리다이렉트)한다.

1. url:/event(요청)
> GET /event HTTP/1.1  
> Host: localhost:8080  

2. 응답
> HTTP/1.1 301 Moved Permanently  
> Location: /new-event 

3.url:/new-event(자동 리다이렉트)

4.요청
> GET /new-event HTTP/1.1  
> Host: localhost:8080  

5.응답
> HTTP/1.1 200 OK  
> ... 

### 리다이렉션 종류

- 영구 리다이렉션 - 특정 리소스의 URI가 영구적으로 바뀜
  - 예) /members --> /users
  - 예) /event -> /new-event
- 일시 리다이렉션 - URI가 일시적으로 바뀜
  - 주문 완료 후 주문 내역 화면으로 이동
  - PRG: POST/Redirect/Get
- 특수 리다이렉션 
  - 결과 대신 캐시를 사용

### 영구 리다이렉션 - 301, 308

- 리소스의 URI를 영구적으로 이동
- 원래의 URI는 사용하지 x, 검색 엔진 등에서도 변경을 감지함
- 301 Moved Permanently
  - 리다이렉트시 요청 메소드가 GET으로 변하고, 본문이 제거될 수 있음(may)
- 308 Permanently Redirect
  - 301과 기능은 같음
  - 리다이렉트시 요청 메소드와 본문을 유지함(처음 post를 보내면 리다이렉트도 post 유지)

### 영구 리다이렉션 - 301

1. Post 사용(요청)
> POST /event HTTP/1.1  
> Host: localhost:8080  
>   
> name=hello&age=20 

2. 응답
> HTTP/1.1 301 Moved Permanently  
> Location: /new-event

3. 자동 리다이렉트
- url:/new-event

4. GET으로 변경(요청)
> GET /new-event HTTP/1.1  
> Host: localhost:8080  

5. 응답 

### 영구 리다이렉션 - 308

1. Post 사용(요청)
> POST /event HTTP/1.1  
> Host: localhost:8080
>
> name=hello&age=20

2. 응답
> HTTP/1.1 308 Permanent Redirect 
> Location: /new-event

3. 자동 리다이렉트
- url:/new-event

4. POST 유지(요청)
> POST /new-event HTTP/1.1  
> Host: localhost:8080  
>   
> name=hello&age=20

5. 응답 


### 일시적인 리다이렉션 - 302, 307, 303

- 리소스의 URI가 일시적으로 변경
- 따라서 검색엔진 등에서 url을 변경하면 안됨
- 302 Found
  - 리다이렉트시 요청 메소드가 GET으로 변하고, 본문이 제거될 수 있음(may)
- 307 Temporary Redirect
  - 302와 기능은 같다
  - 리다이렉트 요청 메소드와 본문이 유지된다.(요청 메소드를 바꾸면 안된다.)
- 303 See Other
  - 302와 기능이 같다
  - 리다이렉트시 요청 메소드가 GET으로 변경된다.

### PRG:POST/REDIRCT/GET

- 일시적인 리다이렉션
- POST로 주문후에 웹브라우저를 새로고침하면?
- 새로고침은 다시 요청이다
- 중복 주문이 될 수 있다.
- POST로 주문후에 새로고침으로 인한 중복 주문을 방지한다.
- POST로 주문후에 주문 결과 화을 GET 메소드로 리다이렉트
- 새로고침해도 결과 화면을 GET으로 조회한다.
- 중복 주문 대신에 결과 화면만 GET으로 다시 요청한다.

### PRG 사용전

1. url:/order(post요청)
> POST /order HTTP/1.1  
> Host: localhost:8080  
>   
> itemId=chicken&count=1

2. 주문데이터 저장
- chicken 1개

3. 응답
> HTTP/1.1 200 OK  
>   
> \<html>주문완료\</html>

4. url:/order(결과 화면에서 새로고침(=다시요청))
5. 요청
> POST /order HTTP/1.1  
> Host: localhost:8080
>
> itemId=chicken&count=1

6. 주문데이터 저장
- chicken 1개

7. 응답
> HTTP/1.1 200 OK
>
> \<html>주문완료\</html>


### PRG 사용 후

1. url:/order(요청)
> POST /order HTTP/1.1  
> Host: localhost:8080  
>   
> itemId=chicken&count=1

2. 주문데이터 저장
- chicken 1개

3. 응답
> HTTP/1.1 302 Found  
> Location: /order-result/19  

4. url:/order-result/19(자동 리다이렉트)

5. 요청 
> GET /order-result/19 HTTP/1.1  
> Host: localhost:8080

6. 주문 데이터 조회
- 19번 주문

7. 응답
> HTTP/1.1 200 OK  
>   
> /<h/tml/>주문완료</html/> 

8. 결과 화면에서 새로고침
- 5번 요청으로 이동 

- PRG 이후 리다이렉트
- URL이 이미 post -> get으로 리다이렉트 됨
- 새로고침 해도 get으로 결과 화면만 조회

### 그래서 뭘 사용해야 되나요?

- 잠깐 정리
  - 302 Found - GET으로 변할 수 있음
  - 307 Temporary Redirect 메소드가 변하면 안됨
  - 303 See Other - 메소드가 GET으로 변경
- 역사
  - 처음 302 스펙의 의도는 HTTP 메소드르 유지하는 것
  - 그런데 웹 브라우저들이 대부분 GET으로 바꾸어버림(일부는 다르게 동작)
  - 그래서 모호한 302 대신 명확한 307, 303이 등장함(301대응으로 308도 등장)
- 현실
  - 307, 303을 권장하지만 현실적으로 이미 많은 애플리케이션 라이브러리들이 302를 기본값으로 사용
  - 자동 리다이렉션시에 GET으로 변해도 되면 그냥 302 사용해도 큰 문제 없음 

### 기타 리다이렉션 

- 300 Multiple Choice: 사용 안함
- 304 Not Modified
  - 캐시 목적으로 사용
  - 클라이언트에게 리소스가 수정되지 않았음을 알려준다. 따라서 클라이언트는 로컬 PC에 저장된 캐시를 재사용한다.(캐시를 리다이렉트한다.)
  - 304 응답은 응답에 메세지 바디를 포함하면 안된다.(로컬 캐시를 사용해야 하므로)
  - 조건부 GET, HEAD 요청시에 사용한다.

## 4xx(클라이언트 오류)

- 클라이언 요청의 잘못된 문법등으로 인해 서버가 요청을 처리할 수 없음
- 오류의 원인은 클라이언트
- 이미 요청이 잘못된 것이므로 다시 시도해도 또 실패한다.

### 400 Bad Request 

- 요청 구문, 메세지 등 오류
- 클라이언트는 요청 내용을 검토하고 다시 보내야 한다.
- 예) 요청 파라미터가 잘못되거나, API 스펙이 맞지 않을 때

### 401 Unauthorized

- 클라이언트가 해당 리소스에 인증(Authentication)이 필요함(=인증되지 않음)
- 401 오류 발생 시 응답이 WWW-Authenticate 헤더와 함께 인증 방법을 설명
- 참고
  - 인증(Authentication): 본인이 누구인지 확인하는 것 - 로그인
  - 인가(Authorization): 권한을 부여하는 것 (ADMIN처럼 특정 리소스에 접근할 수 있는 권, 인증이 있어야 인가를 할 수 있다.)
  - 오류 메세지에 Unauthorized이지만 인증이 되지않은 것(이름이 아쉽다)

### 403 Forbidden

- 서버가 요청을 이해했지만 승인을 거부함을 나타냄
- 주로 인증은 됐지만 접근 권한이 불충분한 경우일 때 발생
- 예) 어드민 등급이 아닌 사용자가 로그인은 했지만, 어드민 등급의 리소스에 접근하는 경우

### 404 Not Found

- 요청 리소스를 찾을 수 없음
  - 요청 리소스가 서버에 없어서,
  - 또는 클라이언트가 권한이 없는 리소스에 접근할 떄 해당 리소스를 숨기고 싶을 때


## 5xx(서버 오류)

- 서버에 문제가 있음
- 서버에 문제가 있기 때문에 재시도(다시 요청)하면 성공할 수도 있음(복구가 되거나 등등)

### 500 Internal Server Error

- 서버 문제로 오류 발생 애매하면 500 오류 

### 503 Service Unavailable 

- 서비스 이용 불가
- 서버가 일시적인 과부하 또는 예정된 작업으로 잠시 요청을 처리할 수 없음
- Retry-After 헤더 필드로 얼마뒤에 복구되는지 보낼 수도 있음

