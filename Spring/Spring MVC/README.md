# Spring MVC

## 목차

- [웹 서버 & 웹 애플리케이션 서버](#웹-서버--웹-애플리케이션-서버)
- [서블릿](#서블릿)
- [동시 요청 - 멀티 쓰레드](#동시-요청---멀티-쓰레드)
- [SSR & CSR](#ssr--csr)
- [redirect vs forward](#redirect-vs-forward)
- [Spring MVC](#spring-mvc)
- [@Controller vs @RestController](#controller-vs-restController)
## 정리할 것들
- Filter와 Interceptor 차이

---

## 웹 서버 & 웹 애플리케이션 서버

### 1. 웹 서버(Web Server)

- HTTP 기반으로 동작
- 클라이언트가 요청하는 정적 리소스를 제공한다.
  - 정적 리소스 : 정적(파일) HTML, CSS, JS, 이미지, 영상
- 예) NGINX, APACHE

### 2. 웹 애플리케이션 서버(WAS, Web Application Server)

- HTTP 기반으로 동작
- 프로그램 코드를 실행해서 애플리케이션 로직 수행
    - 동적 HTML, HTTP API(JSON)
    - 서블릿, JSP, 스프링 MVC
- 웹 서버 기능 포함
- 예) 톰캣, Jetty, Undertow

### 3. 차이점

- 웹 서버는 정적 리소스(파일)를 제공하고, WAS는 애플리케이션 로직을 수행한다.
- 하지만 웹 서버가 프로그램 실행 기능을 포함하기도 하고, WAS가 웹 서버의 기능을 제공하기도 한다.
- WAS는 애플리케이션 코드를 실행하는데 특화되어 있다고 보면 된다.
- 자바는 서블릿 컨테이너 기능을 제공하면 WAS이다.
    - 하지만 서블릿 없이 자바 코드를 실행하는 서버 프레임워크도 있다.

### 4. 웹 시스템 구성

![image](https://user-images.githubusercontent.com/87891581/148025065-0830c2ff-6298-425a-964a-66015785b9f5.png)

- 정적 리소스는 웹 서버가 처리하고, 애플리케이션 로직같은 동적인 처리가 필요하면 웹 서버가 WAS에게 요청을 위임한다.
- WAS와 DB 만으로 시스템 구성이 가능하다. 하지만 아래와 같은 한계가 있다.
    - WAS가 너무 많은 역할을 담당, 서버 과부하 우려
    - 가장 비싼 애플리케이션 로직이 정적 리소스 때문에 수행이 어려울 수 있다.
    - WAS 장애시 오류 화면도 노출 불가능

#### 장점

- 효율적인 리소스 관리
    - 정적 리소스가 많이 사용되면 Web 서버 증설
    - 애플리케이션 리소스가 많이 사용되면 WAS 증설
- WAS, DB 장애시 Web 서버가 오류 화면 제공 가능
    - 정적 리소스만 제공하는 웹 서버는 잘 죽지 않음.

## 서블릿

- 클라이언트의 요청을 처리하고, 결과를 반환하는 자바 웹 프로그래밍 기술이다.
- 프론트엔드의 요청을 응답하기 위해서는 비즈니스 로직 실행 뿐만 아니라 TCP/IP 연결, HTTP 요청 메시지 파싱 및 내용 해석, 응답 메시지 작성 등의 여러 과정이 존재한다.
- 서블릿을 지원하는 WAS를 사용한다면, 개발자는 비즈니스 로직만 신경쓰면 된다.

### 1. HTTP 요청, 응답 흐름

![image](https://user-images.githubusercontent.com/87891581/148026205-20013787-499d-499e-98c3-350f5afaa8c4.png)

1. HTTP 요청
2. WAS는 Request, Response 객체를 새로 만들어서 URL에 맞는 서블릿 객체 호출
3. 개발자는 Request 객체(HttpServletRequest)에서 HTTP 요청 정보를 편리하게 꺼내서 사용
4. 개발자는 Response 객체(HttpServletResponse)에 HTTP 응답 정보를 편리하게 입력
5. WAS는 Response 객체에 담겨있는 내용으로 HTTP 응답 정보를 생성

### 2. 서블릿 컨테이너

![image](https://user-images.githubusercontent.com/87891581/148026414-160e27e4-7ee6-4b1f-8632-122396aa0994.png)

- 톰캣처럼 서블릿을 지원하는 WAS를 서블릿 컨테이너라고 한다.
- 서블릿 컨테이너는 서블릿 객체를 생성, 초기화, 호출, 종료하는 생명주기 관리
  - 서블릿 컨테이너 종료시 함께 종료
- 서블릿 객체는 싱글톤 관리
  - 요청마다 객체를 생성하는 것은 비효율적이다.
  - 모든 요청은 동일한 서블릿 객체 인스턴스에 접근
- JSP도 서블릿으로 변환되어서 사용
- 동시 요청을 위한 멀티 쓰레드 처리 지원

## 동시 요청 - 멀티 쓰레드

- 멀티 쓰레드 부분도 WAS가 처리해주기 때문에 편리하게 소스 코드를 개발할 수 있다.
- 멀티 쓰레드 환경이므로 싱글톤 객체(서블릿, 스프링 빈)는 주의해서 사용한다.

### 1. 쓰레드

- 애플리케이션 코드를 하나하나 순차적으로 실행하는 것이 쓰레드이다.
  - 한번에 하나의 코드 라인만 수행
- 자바 메인 메서드를 처음 실행하면 main이라는 이름의 쓰레드가 실행
- 쓰레드가 없다면 자바 애플리케이션 실행 불가능
- 하나의 요청을 하나의 쓰레드가 담당
  - 동시 처리가 필요하면 쓰레드를 추가로 생성

### 2. 동시 처리 해결방안

#### 1) 요청마다 쓰레드 생성

- 장점
  - 동시 요청 처리 가능
  - 리소스(CPU, 메모리)가 허용할 때 까지 처리 가능
  - 하나의 쓰레드가 지연되어도, 나머지 쓰레드는 정상 동작한다.
- 단점
  - 쓰레드는 생성 비용이 매우 비싸다
    - 고객 요청이 올 때마다 쓰레드를 생성하면, 응답 속도가 늦어진다.
  - 쓰레드는 컨텍스트 스위칭 비용이 발생한다.
    - CPU는 여러 쓰레드를 번갈아가면서 실행한다.
  - 쓰레드 생성에 제한이 없다.
    - 요청이 너무 많으면 CPU, 메모리 임계점을 넘어서 서버가 죽을 수 있다.

#### 2) 쓰레드 풀

- 특징
  - 필요한 쓰레드를 쓰레드 풀에 보관하고 관리
  - 쓰레드 풀에 생성 가능한 쓰레드의 최대치를 관리한다. 톰캣은 최대 200개 기본설정(변경 가능)
  - 최대 쓰레드가 모두 사용중이어서 쓰레드 풀에 쓰레드가 없다면, 기다리는 요청을 거절하거나 특정 숫자만큼만 대기하도록 설정할 수 있다.
- 장점
  - 쓰레드가 미리 생성되어 있으므로, 쓰레드를 생성하고 종료하는 비용(CPU)이 절약되고, 응답 시간이 빠르다.
  - 생성 가능한 최대치가 존재하므로, 너무 많은 요청이 들어와도 기존 요청은 안전하다.

#### 실무 팁

- WAS의 주요 튜닝 포인트는 최대 쓰레드 수이다.
- 너무 낮게 설정하면, 동시 요청이 많을 때 서버 리소스는 여유롭지만 응답이 지연된다.
- 너무 높게 설정하면, 동시 요청이 많을 때 CPU, 메모리 리소스 임계점 초과로 서버가 다운된다.
- 장애 발생시
  - 클라우드라면, 서버부터 늘리고 이후에 튜닝
  - 클라우드가 아니라면, 열심히 튜닝
- 적정 값은 애플리케이션 로직의 복잡도, CPU, 메모리, IO 리소스 상황에 따라 모두 다르다.
  - 최대한 실제 서비스와 유사하게 성능 테스트 시도
    - 툴 : 아파치 ab, 제이미터, nGrinder

## SSR & CSR
### SSR
- 서버 사이드 렌더링
- HTML 최종 결과를 서버에서 만들어서 웹 브라우저에 전달
- 주로 정적인 화면에 사용
- 관련 기술 : JSP, 타임리프

### CSR
- HTML 결과를 자바스크립트를 사용해 웹 브라우저에서 동적으로 생성해서 적용
- 주로 동적인 화면에 사용, 웹 환경을 마치 앱처럼 필요한 부분을 변경할 수 있음
- 관련 기술 : React, Vue.js

### 참고
- CSR, SSR을 동시에 지원하는 웹 프레임워크도 있다.
- SSR을 사용하더라도, 자바스크립트를 사용해서 화면 일부를 동적으로 변경 가능

## redirect vs forward
- 리다이렉트는 클라이언트로 요청에 대한 응답이 나갔다가, redirect 경로로 새로 요청하는 것이다.
  - 클라이언트가 인지할 수 있고, URL 경로도 실제로 변경된다.
- 포워드는 서블릿이나 JSP가 요청을 받은 우 다른 서블릿이나 JSP로 처리를 위임하는 것이다.
  - 서버 내부에서 일어나는 호출이기 때문에 클라이언트가 전혀 인지하지 못한다.

## Spring MVC
- Spring MVC란 Front Controller 패턴에 기초한 웹 MVC 프레임워크이다.

### MVC 패턴
- 서블릿으로만 개발한다면, 뷰 화면을 위한 HTML을 만드는 작업이 자바 코드에 섞여서 지저분하고 복잡하다.
- HTML 작업을 편리하게 하기 위해 JSP를 사용하더라도, 코드가 복잡하고 유지보수가 어렵다는 문제는 유효하다.
- 이에 대한 해결 방안으로 비즈니즈 로직은 Controller로, 화면을 그리는 일은 View로 분리한 다음에 뷰가 필요한 데이터는 Model에 담아서 넘기는 방법이 등장하였다.
  - 이를 MVC 패턴이라고 한다.
  - 컨트롤러 : HTTP 요청을 받아서 파라미터를 검증하고, 비즈니스 로직을 실행한다. 그리고 뷰에 전달한 결과 데이터를 조회해서 모델에 담는다.
  - 모델 : 뷰에 출력할 데이터를 담아둔다.
  - 뷰 : 모델에 담겨있는 데이터를 사용해서 화면을 그리는 일에 집중한다.

### Front Controller 패턴
- 프론트 컨트롤러 서블릿 하나로 클라이언트 요청을 받고, 그에 맞는 컨트롤러를 찾아서 호출한다.
- 여러개의 서블릿으로 처리할 때 중복되는 코드을 하나로 묶어서 관리한다.
  - 중복되는 코드 : view로 포워드, prefiex, suffix
  - 간혹 사용하지 않는 request, response 객체도 존재한다.

### 어댑터 패턴
- 프론트 컨트롤러가 다양한 방식의 컨트롤러를 처리할 수 있게 만든다.
- 프론트 컨트롤러는 어댑터만 있다면 어떤 것이든 처리할 수 있기 때문에 컨트롤러 대신 핸들러라는 명칭을 사용한다.

### 동작 순서
![image](https://user-images.githubusercontent.com/87891581/168423149-d198ea93-908f-4c09-85b2-8b43e527f13c.png)
1. 핸들러 조회 : 클라이언트가 요청을 보내면, Dispatcher Servlet에서 핸들러 매핑을 통해 요청 URL에 매핑된 핸들러(컨트롤러)를 조회한다.
2. 핸들러 어댑터 조회 : 핸들러를 실행할 수 있는 핸들러 어댑터를 조회한다.
3. 핸들러 어댑터 실행 : 핸들러 어댑터를 실행한다.
4. 핸들러 실행 : 핸들러 어댑터가 실제 핸들러를 실행한다.
5. ModelAndView 반환 : 핸들러 어댑터는 핸들러가 반환하는 정보를 ModelAndView로 변환해서 반환한다.
6. viewResolver 호출 : 뷰 리졸버를 찾아 실행한다.
7. View 반환 : 뷰 리졸버는 뷰의 논리 이름을 물리 이름으로 바꾸고, 뷰 객체를 반환한다.
8. 뷰 렌더링 : 뷰에 Model을 보내고 렌더링한다.
9. 완성된 뷰를 클라이언트에 보내서 화면에 출력한다.

## @Controller vs @RestController
- `@Controller`는 반환 값이 String이면 뷰 이름으로 인식된다. 그래서 뷰를 찾고 뷰가 렌더링된다.
- `@RestController`는 `@ResponseBody`와 `@Controller`가 결합되었다.
- `@RestController`는 반환값으로 뷰를 찾는 것이 아니라, HTTP 메시지 바디에 바로 입력한다.
  - 따라서 실행 결과로 ok 메세지를 받을 수 있다.