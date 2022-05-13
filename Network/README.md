# Network

## 목차
- [OSI 7계층 & TCP/IP 4계층](#osi-7계층--tcpip-4계층)
- [TCP/IP](#tcpip)
- [IP(인터넷 프로토콜)](#ip인터넷-프로토콜)
- [TCP & UDP](#tcp--udp)
- [3-way handshake & 4-way handshake](#3-way-handshake--4-way-handshake)
- [PORT](#port)
- [DNS](#dns)
- [URI, URL, URN](#uri-url-urn)
- [웹 브라우저 요청 흐름](#웹-브라우저-요청-흐름)
- [HTTP](#http)
- [HTTPS](#https)
- [HTTP 메서드](#http-메서드)
- [클라이언트에서 서버로 데이터를 전송하는 방법](#클라이언트에서-서버로-데이터를-전송하는-방법)
- [HTTP API 설계 예시](#http-api-설계-예시)
- [HTTP 상태 코드](#http-상태-코드)
- [쿠키 & 세션](#쿠키--세션)

## 정리할 것들
- API, URI 등
- 캐시
---

## OSI 7계층 & TCP/IP 4계층
![image](https://user-images.githubusercontent.com/87891581/168009131-3d8a50ae-b638-4f41-9567-300603b98aa4.png)
### 1. OSI 7계층
- 국제 표준화 기구(ISO)에서 개발한 모델로, 컴퓨터 네트워크 프로토콜 디자인과 통신을 계층으로 나누어 설명한 것이다.
- 통신이 일어나는 과정을 단계별로 알 수 있고, 특정한 곳에 이상이 생기면 그 단계만 수정할 수 있기 때문에 편리하다.

**1. 물리 계층(Physical layer)**
> 리피터, 케이블, 허브 등

- 주로 전기적, 기계적, 기능적인 특성을 이용해서 통신 케이블로 데이터를 전송하는 역할을 한다.  

**2. 데이터 링크 계층(Data link layer)**
> 브릿지, 스위치 등

- 물리 계층을 통해 송, 수신되는 정보의 오류와 흐름을 관리하여 안전한 정보의 전달을 수행할 수 있도록 도와주는 역할을 한다.
- MAC 주소를 이용해 통신한다.
- Frame에 MAC 주소를 부여하고 에러검출, 재전송, 흐름 제어를 진행한다.

**3. 네트워크 계층(Network layer)**  
> 라우터, IP

- 데이터를 목적지까지 가장 안전하고 빠르게 전달하는 기능을 담당한다.
- 라우터를 통해 이동할 경로를 선택하여 IP 주소를 지정하고, 해당 경로에 따라 패킷을 전달해준다.
- 라우팅, 흐름 제어, 오류 제어, 세그먼테이션 등을 수행한다.

**4. 전송 계층(Transport layer)**  
> TCP, UDP

- TCP, UDP 프로토콜을 통해 통신을 활성화 한다. 
  - TCP : 신뢰성, 연결 지향적
  - UDP : 비신뢰성, 비연결성, 실시간
- 포트를 열어두고, 프로그램들이 전송을 할 수 있도록 제공해준다. 
- 이를 통해 양 끝 단의 사용자들이 데이터를 주고 받을 수 있다.

**5. 세션 계층(Session layer)**  
> API, Socket

- 데이터가 통신하기 위한 논리적인 연결을 말한다.
- 양 끝단의 응용 프로세스가 통신을 관리하기 위한 방법을 제공한다.
- TCP/IP 세션을 만들고 없애는 책임을 지니고 있다.

**6. 표현 계층(Presentation layer)**  
- 데이터 표현에 대한 독립성을 제공하고 암호화하는 역할을 담당한다.
- 해당 데이터가 TEXT인지, 그림인지, GIF인지, JPG인지 등의 구분이 표현 계층이 하는 일이다.
- 코드 간의 번역을 담당하여 사용자 시스템에서 데이터의 형식상 차이를 다루는 부담을 응용 계층으로부터 덜어준다.

**7. 응용 계층(Application layer)**  
> HTTP, FTP 등

- 최종 목적지로, 응용 프로세스와 직접 관계하여 일반적인 응용 서비스를 수행한다.

### 2. TCP/IP 4계층
**1. 네트워크 인터페이스 계층**
- OSI 계층의 물리 계층과 데이터 링크 계층에 해당된다.
- 신뢰성 있는 데이터 전송을 담당한다.
- 물리적인 주소로 MAC을 사용한다.

**2. 인터넷 계층**
- OSI 계층의 네트워크 계층에 해당된다.

**3. 전송 계층**
- OSI 계층의 전송 계층에 해당된다.

**4. 애플리케이션 계층 - HTTP, FTP**
- OSI 계층의 세션 계층, 표현 계층, 응용 계층에 해당된다.
- 다른 계층의 서비스에 접근할 수 있게 하는 애플리케이션을 제공한다.
- 응용프로그램(application)들이 데이터를 교환하기 위해 사용하는 프로토콜을 정의한다.

## TCP/IP
- TCP와 IP 두 가지 프로토콜로 이루어져 있다.
- 데이터가 의도된 목적지에 닿을 수 있도록 보장해주는 통신 규약이다.

## IP(인터넷 프로토콜)
- 컴퓨터 네트워크에서 장치들이 서로를 인식하고 통신을 하기 위해서 사용하는 특수한 번호이다.
- 주로 사용하는 주소는 IPv4(32비트) 주소이며, 시간이 갈수록 IPv4 주소의 부족으로 128비트의 IPv6 주소가 등장했다.
- 지정한 IP 주소(IP Address)에 패킷(Packet)이라는 통신 단위로 데이터 전달
- IP 패킷
  ![image](https://user-images.githubusercontent.com/87891581/147866287-cf9593db-7932-43d7-9edd-c301e02123ce.png)
### 한계점
- 비연결성
    - 패킷을 받을 대상이 없거나 서비스 불능 상태여도 패킷을 전송한다.
- 비신뢰성
    - 중간에 패킷이 유실될 수 있다.
    - 패킷이 순서가 바뀔 수 있다.
- 프로그램 구분
    - 같은 IP를 사용하는 서버에서 통신하는 애플리케이션을 구분할 수 없다.

## TCP & UDP
- 전송 계층에서 사용하는 프로토콜
### 1. TCP
- 전송 제어 프로토콜(Transmission Control Protocol)
- 신뢰성 있는 데이터 전송을 지원하는 연결 지향형 프로토콜
- 사전에 3-way handshake라는 과정을 통해 통신을 시작하고, 4-way handshake 과정으로 통해 연결을 해제한다.
  - 가상 회선 방식이라고 부른다.
- TCP가 가상 회선 방식을 제공한다는 것은 송신측과 수신측을 연결하여 패킷을 전송하기 위한 논리적 경로를 배정한다는 뜻이다.
- 흐름 제어, 혼잡 제어를 통해 신뢰성을 보장한다. 
  - 흐름 제어
    - 데이터를 송식하는 곳과 수신하는 곳의 데이터 처리 속도를 조절하여 수신자의 버퍼 오버플로우를 방지하는 것이다.
    - 송신하는 곳에서 감당이 안되게 많은 데이터를 빠르게 보내 수신하는 곳에서 문제가 발생하는 것을 막는다.
  - 혼잡 제어
    - 네트워크 내의 패킷 수가 넘치지 않게 방지하는 것이다.
    - 정보의 소통량이 과다하면 패킷을 조금만 전송해서 혼잡 붕괴 현상이 발생하는 것을 막는다.
- UDP보다 속도가 느리다.
- 현재는 대부분 TCP 사용  

**TCP/IP 패킷**
![image](https://user-images.githubusercontent.com/87891581/147866498-90715019-50e8-4f3b-b3f3-60b7e731d225.png)

### 2. UDP
- 사용자 데이터그램 프로토콜(User Datagram Protocol)
- 데이터를 데이터그램 단위로 처리하는 비연결형 프로토콜
- 연결을 위해 할당하는 논리적인 경로가 없다.
  - 각각의 패킷은 다른 경로로 전송되고, 독립적으로 처리된다.
  - 순서가 뒤바뀔 수도 있기 때문에 애플리케이션에서 추가 작업이 필요하다.
- 속도가 빠르고 네트워크 부하가 적기 때문에 성능 향상을 위해 UDP의 사용 빈도 증가

## 3-way handshake & 4-way handshake
### 1. 3-way handshake
- TCP/IP 프로토콜로 통신을 진행할 때, 두 종단 간 정확한 데이터 전송을 보장하기 위해 연결을 설정하는 과정이다.

#### 연결 과정
1. 클라이언트는 서버에 적속을 요청하는 SYN 패킷을 보낸다.
2. 서버는 요청 수락 응답으로 ACK 패킷과 클라이언트도 포트를 열어달라는 SYN 패킷을 보낸다.
3. 클라이언트는 이에 대한 수락 응답으로 ACK 패킷을 보내며 가상 연결이 성립된다.

### 2. 4-way handshake
- TCP/IP 프로토콜에서는 3 way handshake로 연결을 설정하고, 4 way handshake로 연결 설정을 해제한다.

#### 연결 과정
1. 클라이언트는 서버에게 연결을 종료하겠다는 FIN 패킷을 보낸다.
2. 서버는 확인했다는 응답으로 ACK 패킷을 보낸다.
   - 이때 모든 데이터를 보내기 위해 CLOSE_WAIT 상태가 된다.
3. 데이터를 모두 보냈다면, 연결을 종료하겠다는 FIN 패킷을 클라이언트에게 보낸다.
4. 클라이언트는 확인했다는 응답으로 ACK 패킷을 보낸다.
  - 서버로부터 받지 못한 데이터가 있을 수 있으므로 TIME_WAIT 상태로 기다린다.
5. 서버는 ACK를 받인 이후 소켓을 닫는다.(Closed)
6. 클라이언트는 TIME_WAIT 상태가 끝나면 소켓을 닫는다.(Closed)

## PORT

- 같은 IP 내에서 프로세스 구분하기 위해 사용한다.
    - 아파트 동 -> IP, 호수 -> PORT
- 0 ~ 65535 할당 가능(2^16)
- 0 ~ 1023 잘 알려진 포트, 사용하지 않는 것이 좋다.
    - FTP - 20, 21
    - TELNET - 23
    - HTTP - 80
    - HTTPS - 443

## DNS
- 도메인 네임 시스템(Domain name System)
- IP 주소를 문자로 표현한 주소를 도메인 네임이라고 한다.
- IP는 기억하기 어렵고, 변경될 수 있기 때문에 사용한다.
- DNS 서버에서 도메인 네임과 매칭되는 IP 주소값을 보유하고 있다.

## URI, URL, URN

### 1. URI

- Uniform Resource Identifier
    - Uniform : 리소스를 식별하는 통일된 방식
    - Resource : 자원, URI로 식별할 수 있는 모든 것(제한 없음)
    - Identifier : 다른 항목과 구분하는데 필요한 정보
- 인터넷에 있는 자원을 나타내는 유일한 주소이다.
- URL과 URN이 URI에 포함된다.
  ![image](https://user-images.githubusercontent.com/87891581/147871549-b5e50fdc-4e0f-46d3-aa44-f413560f6394.png)

### 2. URL과 URN

![image](https://user-images.githubusercontent.com/87891581/147871575-1fbe4958-30f3-45f8-b08d-91c6ff0a46d5.png)

- URL - Locator : 리소스가 있는 위치 지정
- URN - Name : 리소스에 이름을 부여
    - 예 urn:isbn:896077731
- 위치는 변할 수 있지만, 이름은 변하지 않는다.
- URN 이름만으로 실제 리소스를 찾을 수 있는 방법이 보편화 되지 않음

### 3. URL 문법

`scheme://[userinfo@]host[:port][/path][?query][#fragment]`  
- ex) `https://www.google.com:443/search?q=hello&hl=ko`
- scheme
    - 주로 프로토콜을 사용
    - 프로토콜 : 어떤 방식으로 자원에 접근할 것이가 하는 약속 규칙. 예) http, https, ftp 등
        - https는 http에 보안 추가(HTTP Secure)
- userinfo
    - URL에 사용자 정보를 보항해서 인증
    - 거의 사용하지 않음
- host
    - 호스트명
    - 도메인명 또는 IP 주소를 직접 사용 가능
- port
    - 접속 포트
    - 일반적으로 생략.
    - http는 80포트, https는 443 포트를 주로 사용.
- path
    - 리소스 경로(path)
    - 계층적 구조
    - 예)
        - `/home/file1.jpg`
        - `/members`
- query
    - `key=value` 형태
    - ?로 시작, &로 추가 가능
        - 예) ?keyA = valueA&keyB=valueB
    - query parameter, query string등으로 불림.
    - 문자 형태
- fragment
    - html 내부 북마크 등에 사용
    - 서버에 전송하는 정보 아님

## 웹 브라우저 요청 흐름

<img src="https://user-images.githubusercontent.com/87891581/168077028-da2d1d67-6b73-4a5f-a5c1-98d7c3c3da1c.png" alt="이미지">

1. 클라이언트가 도메인 명(ex. google.com)을 포함하는 URL로 요청한다.
2. DNS 서버에서 도메인 명과 매칭과는 IP 주소를 찾는다.
3. 브라우저는 DNS를 통해 서버의 진짜 주소를 찾음
4. HTTP 프로토콜을 사용하여 HTTP 요청 메세지를 생성한다.
5. TCP/IP 연결을 통해 HTTP 요청이 인터넷을 거쳐 해당 IP 주소의 서버로 전송된다.
6. 서버는 HTTP 프로토콜을 활용하여 적절한 데이터를 찾고, HTTP 응답 메세지를 생성한다.
7. TCP/IP 연결을 통해 요청한 컴퓨터로 전송
8. 도착한 HTTP 응답 메세지는 HTTP 프로토콜을 활용하여 웹페이지 데이터로 변환되고, 웹 브라우저에 의해 출력되어 사용자가 볼 수 있게 된다.

## HTTP

- HyperText Transfer Protocol
- 인터넷 상에서 클라이언트와 서버가 자원을 주고 받을 때 사용하는 통신 규약
  - 서버간에 데이터를 주고 받을 때도 대부분 HTTP 사용
- 거의 모든 형태의 데이터 전송 가능
    - HTML, TEXT
    - IMAGE, 음성, 영상, 파일
    - JSON, XML (API)
- 주로 TCP 기반의 통신 방식
- 특징
  - 클라이언트 서버 구조
  - 무상태 프로토콜
  - 비연결성
  - HTTP 메시지
  - 단순하고 확장 가능

### 1. 기반 프로토콜

- TCP : HTTP/1.1(가장 많이 사용), HTTP/2
- UDP : HTTP/3

### 2. 특징

#### 1) 클라이언트 서버 구조

- Request Response 구조
- 클라이언트는 서버에 요청을 보내고, 응답을 대기
- 서버가 요청에 대한 결과를 만들어서 응답

#### 2) 무상태 프로토콜(stateless)

- 서버가 클라이언트의 상태를 보존하지 않는다.
    - 중간에 서버가 변경되어도 요청과 응답에 지장이 없다.
- 모든 것을 무상태로 설계할 수 없는 경우도 있다.
  - ex) 로그인을 하는 경우 로그인한 상태를 서버에서 유지해야한다.
  - 브라우저 쿠키와 서버 세션 등을 사용해서 상태 유지
  - 상태 유지는 최소한만 사용
- 장점 : 서버 확장성 높음(스케일 아웃)
- 단점 : 클라이언트가 추가 데이터 전송

#### 3) 비연결성
- HTTP는 기본이 연결을 유지하지 않는 모델이다.
- 서버 자원을 효율적으로 사용할 수 있다.
- TCP 기반의 경우 요청할 때마다 연결을 새로 맺어야 한다는 단점이 있지만, HTTP 지속 연결로 최적화를 이루었다.

#### 4) HTTP 메시지
![image](https://user-images.githubusercontent.com/87891581/168089779-753bb923-7180-478f-b3a8-3fd35a864dba.png)
1. start-line
   - request-line(요청 메시지의 경우) : `method SP request-target SP HTTP-version CRLF`
     - HTTP 메서드(ex. `GET`)
     - 요청 대상(ex. `/search?q=hello&hl=ko`)
     - HTTP 버전(ex. `HTTP/1.1`)
   - status-line(응답 메시지의 경우) : `HTTP-version SP status-code SP reason-phrase CRLF`
     - HTTP 버전
     - HTTP 상태 코드 : 요청 성공, 실패를 나타냄 (ex. 200)
     - 이유 문구 : 사람이 이해할 수 있는 짧은 상태코드 설명 글 (ex. OK)
2. HTTP 헤더
   - HTTP 전송에 필요한 모든 부가 정보가 포함된다.
   - ex) 메시지 바디의 크기, 압축, 인증, 요청 클라이언트 정보 등
   - 필요시 임의의 헤더 추가 가능
3. HTTP 메시지 바디
   - 실제 전송할 데이터
   - HTMl 문서, 이미지, 영상, JSON 등 byte로 표현할 수 있는 모든 데이터 전송 가능

#### 5) 단순하고 확장 가능

### 3. 문제점
- HTTP는 평문 통신이기 때문에 도청이 가능하다
- 통신 상대를 확인하지 않기 때문에 위장이 가능하다.
- 완정성을 증명할 수 없기 때문에 변조가 가능하다.  
이러한 문제점을 해결하기 위해 HTTPS가 등장했다.

## HTTPS
- HTTP 통신하는 소켓 부분을 인터넷 상에서 정보를 암호화하는 SSL(Secure Socket Layer)라는 프로토콜로 대체한 것이다.
- HTTP는 TCP와 통신했지만, HTTPS에서 HTTP는 SSL과 통신하고 SSL이 TCP와 통신하게 된다.
  - 하나의 레이어가 추가되었다.
- HTTPS의 SSL에서는 대칭키 암호화 방식과 공개키 암호화 방식을 혼합하여 사용한다.
  - 서버와 클라이언트가 대칭키를 주고받을 때만 공개키 암호화 방식을 사용하고, 이후에는 대칭키 암호화 방식으로 통신한다.
- 민감한 정보를 다룰 때만 HTTPS에 의한 암호화 통신을 사용하는 방식에서, 모든 웹 페이지에 HTTPS를 적용하는 방향으로 바뀌어가고 있다.
  - 평문 통신에 비해서 CPU나 메모리 등 리소스를 더 많이 요구한다.
  - 하지만 최근에는 하드웨어의 발달로 인해 속도 저하가 거의 일어나지 않으며, 새로운 표준인 HTTP 2.0을 함께 이용한다면 오히려 더 빠르게 동작한다. 

### 대칭키 암호화
  ![image](https://user-images.githubusercontent.com/87891581/168204908-fa620507-0ad2-487b-a65f-dc3306387696.png)
- 암호화에 사용되는 키와 복호화에 사용되는 키가 동일한 암호화 기법이다.
- 대칭키 전달 과정에서 해킹 위험에 노출될 수 있다.
- 키 전달 및 관리에 어려움이 있지만, 암호화 연산 속도가 빠르기 때문에 효율적인 암호 시스템을 구축할 수 있다는 장점이 있다.

### 공개키 암호화
- 대칭키 암호화 방식의 키 전달의 취약점을 해결하기 위해 나온 방식이다.
- 암호화에 사용하는 키와 복호화에 사용하는 키를 분리했다.
  - 비대칭키 암호화라고도 부른다.
- 자신이 가지고 있는 고유한 암호키(개인키 혹은 비밀키)로만 복호화 할 수 있는 암호키(공개키)를 대중에게 공개한다.
- 암호화, 복호화를 윈해 복잡한 수학 연산을 수행하기 때문에, 대칭키 방식에 비해 속도가 느리고 복잡하다.

## HTTP 메서드

|Method|설명|
|:--:|--|
|GET|리소스를 조회|
|POST|요청 데이터를 처리, 주로 등록에 사용|
|PUT|리소스가 있으면 대체하고, 없으면 생성한다.|
|PATCH|리소스 부분 변경|
|DELETE|리소스 삭제|
|HEAD|GET과 동일하지만, BODY를 제외하고 상태 줄과 헤더만 반환|
|OPTIONS|대상 리소스에 대한 통신 가능 옵션(메서드)을 설명(주로 CORS에서 사용)|
|CONNECT|대상 자원으로 식별되는 서버에 대한 터널을 설정|
|TRACE|대상 리소스에 대한 경로를 따라 메시지 루프백 테스트를 수행|

**1. GET**
- 리소스 조회
- 서버에 전달하고 싶은 데이터는 query(쿼리 파라미터, 쿼리 스트링)를 통해서 전달
- 메시지 바디를 사용해서 데이터를 전달할 수 있지만, 지원하지 않는 곳이 많아서 권장하지 않는다.

**2. POST**
- 요청 데이터 처리
- 서버는 메시지 바디를 통해 들어온 데이터를 처리하는 모든 기능을 수행한다.
  1. 새 리소스 생성(등록) : 서버가 아직 식별하지 않은 새 리소스 생성
  2. 요청 데이터 처리 : POST 결과로 새로운 리소스가 생성되지 않을 수 있다.
  3. 다른 메서드로 처리하기 애매한 경우 : ex) 조회지만 GET 메서드를 사용하기 어려운 경우
- 주로 신규 리소스 등록, 프로세스 처리에 사용

**3. PUT**
- 리소스가 있으면 대체하고, 없으면 생성한다. 즉, 해당 리소스를 덮어버린다.
- 클라이언트가 리소스를 식별
  - ex) `/members/100`
  - POST와 차이점

**4. PATCH**
- 리소스를 부분 변경
- 지원이 안되는 경우 POST를 사용하면 된다.

**5. DELETE**
- 리소스 제거

### 메서드 속성

|Method|요청에 Body가 있음|응답에 Body가 있음|안전|멱등|캐시 가능|
|:--:|:--:|:--:|:--:|:--:|:--:|
|GET|아니오|예|예|예|예|
|HEAD|아니오|아니오|예|예|예|
|POST|예|예|아니오|아니오|예|
|PUT|예|예|아니오|아니오|예|
|PATCH|예|예|아니오|아니오|예|
|DELETE|아니오|예|아니오|예|아니오|
|OPTIONS|선택 사항|예|예|예|아니오|
|CONNECT|예|예|아니오|아니오|아니오|
|TRACE|아니오|예|예|예|아니오|

**1. 안전(Safe Methods)**
- 호출해도 리소스를 변경하지 않는다.
- Q. 계속 호출해서, 로그 같은게 쌓여서 장애가 발생한다면?
  - A. 안전은 해당 리소스만 고려한다. 그런 부분까지 고려하지 않는다.

**2. 멱등(Idempotent Methods)**
- 한번 호출하든 여러번 호출하든 결과가 동일하다.
- 활용
  - 자동 복구 메커니즘
  - ex) 서버가 정상 응답을 못주었을 때, 클라이언트가 같은 요청을 다시 해도 되는지 판단 근거
- PATCH는 멱등으로 설계할 수 있지만, 아니게도 설계 가능하다.
  - ex) `{"operation": "add", "age": 10}` : 호출할 때마다 10씩 증가
- Q. 재요청 중간에 다른 곳에서 리소스를 변경해 버린다면?
  - A. 멱등은 외부 요인으로 중간에 리소스가 변경되는 것까지 고려하지 않는다.

**3. 캐시가능(Cacheable Methods)**
- 응답 결과 리소스를 캐시해서 사용해도 되는지 여부
- 실제로는 GET, HEAD 정도만 캐시로 사용
  - POST, PATCH는 본문 내용까지 캐시 키로 고려해야 하는데, 구현이 쉽지 않다.

## 클라이언트에서 서버로 데이터를 전송하는 방법
- 쿼리 파라미터를 통한 데이터 전송(GET)
- 메시지 바디를 통한 데이터 전송(POST, PUT, PATCH)

### 1. 정적 데이터 조회
- GET 사용
- 일반적으로 쿼리 파라미터 없이 리소스 경로로 단순하게 조회 가능
- ex) 이미지, 정적 테스트 문서

### 2. 동적 데이터 조회
- GET 사용
- 쿼리 파라미터를 사용해서 데이터 전달
- ex) 조회 조건을 줄여주는 필터, 검색 등

### 3. HTML Form 데이터 전송
- HTML Form submit 시 데이터 전송
- GET, POST만 지원
- POST Content-Type 종류
  - `application/x-www-form-urlencoded`
    - form의 내용을 메시지 바디를 통해서 전송(key=value, 쿼리 파라미터 형식)
    - 전송 데이터를 url encoding 처리
  - `multipart/form-data` 
    - 파일 업로드 같은 바이너리 데이터 전송 시 사용
    - 여러 종류의 파일을 함께 전송 가능

### 4. HTTP API 데이터 전송
- HTTP를 사용해서 서로 정해둔 스펙으로 데이터를 주고 받으며 통신하는 것이다.
- 웹 클라이언트는 자바스크립트로 통신한다.(AJAX)
- GET, POST, PUT, PATCH, DELETE 모두 지원한다.
- Content-Type은 주로 `application/json`을 사용한다.

## HTTP API 설계 예시
- HTTP API - 컬렉션
  - POST 기반 등록 
  - 서버가 리소스 URI 결정(컬렉션)
- HTTP API - 스토어
  - PUT 기반 등록
  - 클라이언트가 리소스 URI 결정(스토어)
- HTML FORM 사용
  - 순수 HTML + HTML form 사용
  - GET, POST만 사용 가능 -> 컨트롤 URI 사용

### URI 설계 개념
**1. 문서(document)**
  - 단일 개념(파일 하나, 객체 인스턴스, 데이터베이스 row)
  - ex) `/members/100`, `/files/start.jpg`

**2. 컬렉션(collection)**
  - 주로 사용
  - 서버가 관리하는 리소스 디렉터리
  - 서버가 리소스의 URI를 생성하고 관리
  - ex) `POST /members`

**3. 스토어(store)**
  - 파일, 게시판 등에 가끔 사용
  - 클라이언트가 관리하는 자원 저장소
  - 클라이언트가 리소스의 URI를 알고 관리
  - ex) `PUT /files/100`

**4. 컨트롤러(controller), 컨트롤 URI**
  - 문서, 컬렉션, 스토어로 해결하기 어려운 추가 프로세스 실행
    - 즉, HTTP 메서드로 해결하기 애매한 경우
  - 동사를 직접 사용
  - ex) `/members/{id}/delete`

## HTTP 상태 코드
- 클라이언트가 보낸 요청의 처리 상태를 응답에서 알려주는 기능
- 클라이언트가 인식할 수 없는 상태 코드를 서버가 반환하면, 상위 상태 코드로 해석해서 처리한다.
  - ex) 299 -> 2xx, 451 -> 4xx
- 종류
  - 1xx(information) : 서버가 요청을 클라이언트에서 성공적으로 수신을 했고, 처리중인 정보를 보낸다.
  - 2xx(Successful) : 서버가 요청을 정상 처리했음을 알린다.
  - 3xx(Redirection) : 요청을 완료하려면 추가 행동이 필요하다.
  - 4xx(Client Error) : 클라이언트 오류, 잘못된 문법 등으로 서버가 요청을 수행할 수 없다.
  - 5xx(Server Error) : 서버 오류, 서버가 클라이언트의 요청을 처리하지 못했다.
### 1xx(information)
- 거의 사용하지 않는다.
### 2xx(Successful)

|code|reason phrase|설명|
|:--:|:--|:--|
|200|OK|성공|
|201|Created|요청을 처리해서 새로운 리소스가 생성됨|
|202|Accepted|요청이 접수되었으나, 처리가 완료되지 않음|
|204|No Content|서버가 요청을 성공적으로 수행했지만, 응답 페이로드 본문에 보낼 테이터가 없음|

### 3xx(Redirection)
- 웹 브라우저는 3xx 응답의 결과에 Location 헤더가 있으면, location 위치로 자동 이동한다.(리다이렉트)

|code|reason phrase|설명|
|:--:|:--|:--|
|300|Multiple Choices|요청에 대해서 하나 이상의 응답 가능하며, 클라이언트는 그 중에 하나를 반드시 선택해야 한다.|
|301|Moved permanently|리다이렉트시 요청 메서드가 GET으로 변하고, 본문이 제거될 수 있음(MAY)|
|302|Found|리다이렉트시 요청 메서드가 GET으로 변하고, 본문이 제거될 수 있음(MAY)|
|303|See Other|리다이렉트시 요청 메서드가 GET으로 변경.|
|304|Not Modified|클라이언트에게 리소스가 수정되지 않았음을 알려준다. 따라서 클라이언트는 로컬 PC에 저장된 캐시를 재사용한다.|
|307|Temporary Redirect|리다이렉트시 요청 메서드와 본문 유지(요청 메서드를 변경하면 안된다. MUST NOT)|
|308|Permanent Redirect|리다이렉트시 요청 메서드와 본문 유지(처음 POST 요청 시 리다이렉트로 POST 유지)|

#### 종류
1. 영구 리다이렉션
   - 리소스의 URI가 영구적으로 이동
   - 원래의 URL을 사용하지 않기 때문에 검색 엔진 등에서 변경을 인지할 수 있다.
   - 301, 308
2. 일시 리다이렉션 : 일시적인 변경
   - 리소스의 URI가 일시적으로 변경
   - PRG
   - 302, 307, 308
     - 307, 303을 권장하지만, 302가 이미 상용화되었다.
3. 특수 리다이렉션
   - 클라이언트에게 리소스가 수정되지 않았음을 알려준다. 따라서 캐시를 재사용한다.
   - 응답 시 메시지 바디를 포함하면 안된다.(로컬 캐시를 사용하기 때문)
   - 조건부 GET, HEAD 요청 시 사용
   - 304

#### PRG
- Post / Redirect / Get
- Post 요청 후 새로 고침으로 인한 중복 처리를 방지하기 위해 GET 메서드로 리다이렉트를 한다.
  - 새로고침 해도 결과 화면을 GET으로 조회

### 4xx(Client Error)
- 요류의 원인이 클라이언트에게 있기 때문에 똑같은 재시도를 하더라도 실패한다.

|code|reason phrase|설명|
|:--:|:--|:--|
|400|Bad Request|클라이언트가 잘못된 요청을 해서 서버가 요청을 처리할 수 없음|
|401|Unauthorized|클라이언트가 해당 리소스에 대한 인증이 필요함|
|403|Forbidden|서버가 요청을 이해했지만, 승인을 거부함|
|404|Not Found|요청 리소스를 찾을 수 없음. 권한이 부족한 리소스에 접근할 때 해당 리소스를 숨기고 싶을 때 사용하기도 함.|

### 5xx(Server Error)
|code|reason phrase|설명|
|:--:|:--|:--|
|500|Internal Server Error|서버 문제로 오류 발생, 애매하면 500 오류|
|503|Service Unavailable|일시적인 과부하, 예정된 작업 등으로 인한 서비스 이용 불가| 

## 쿠키 & 세션
### 등장 배경
- HTTP는 비연결성에 무상태 프로토콜이다. 클라이언트와 서버가 요청과 응답을 주고 받으면, 연결이 끊어지고 서로 상태를 유지하지 않는다.
- 이전 요청과 현재 요청이 같은 사용자의 요청인지 알기 위해서는 상태를 유지해야 한다.
- HTTP에서는 상태를 유지하기 위한 기술로 쿠키와 세션이 있다.

### 쿠키
- 클라이언트의 상태 정보를 키와 값 형태로 로컬에 저장하며, 항상 서버에 전송된다.
  - 네트워크 트래픽을 추가 유발하기 때문에 최소한의 정보만 사용한다.(세션 id, 인증 토큰)
- 이름, 값, 유효 시간, 도메인, 경로 등을 포함한다.
- 세션과 같이 사용하면, 보완에 취약한 점을 보완할 수 있다.

#### 동작 방식
1. 웹 브라우저가 서버에 상태 유지와 관련된 요청
2. 서버가 HTTP 헤더에 Set-Cookie를 포함해서 응답
   - `Set-Cookie: id=홍길동`
3. 웹 브라우저가 전달받은 쿠키를 관리하다가, 다음 요청 시 HTTP 헤더에 쿠키를 포함하여 요청
   - `Cookie: id=홍길동`

### 세션
- 일정 시간 동안 같은 브라우저로부터 들어오는 요청을 하나의 상태로 보고 그 상태를 유지하는 기술이다.
- 서버는 세션 ID와 클라이언트와 관련된 데이터를 서버의 세션 저장소에 키와 값 형태로 보관한다.
- 세션 ID는 예측 불가능하고 만료 시간이 있으며, 서버는 이 세션 ID를 쿠키를 통해 클라이언트에게 전달한다.