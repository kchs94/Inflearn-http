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