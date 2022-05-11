# Spring

## 목차

- [스프링이란](#스프링이란)
- [스프링 부트란](#스프링-부트란)
- [IoC](#IoC)
- [DI](#DI)
- [IoC 컨테이너, DI 컨테이너](#ioc-컨테이너-di-컨테이너)
- [스프링 컨테이너](#스프링-컨테이너)
- [싱글톤 컨테이너](#싱글톤-컨테이너)
- [컴포넌트 스캔](#컴포넌트-스캔)
- [의존 관계 자동 주입](#의존-관계-자동-주입)
- [빈 생명주기 콜백](./빈%20생명주기%20콜백.md)
- [빈 스코프](./빈%20스코프.md)

## 정리할 것들

- Bean이란
- Bean Scope
- MVC 패턴이란
- AOP(Aspect Oriented Programming)란
- POJO
- DAO와 DTO의 차이
- Spring JDBC를 이용한 데이터 접근
- Filter와 Interceptor 차이

---

## 스프링이란

- 스프링은 기업용 온라인 서비스를 지원하기 위한 자바 언어 기반의 프레임워크이다.
- 자바 언어의 가장 큰 특징은 객체 지향 언어라는 것이다.
- 스프링은 [객체 지향 언어가 가진 가장 강력한 특징](../OOP/객체%20지향%20프로그래밍.md)을 살려내는 프레임워크.
- [좋은 객체 지향 애플리케이션](../OOP/SOLID.md)을 개발할 수 있게 도와주는 프레임워크.

## 스프링 부트란

- 스프링을 복잡한 설정 없이 쉽고 빠르게 만들어주는 라이브러리이다.
- 특징
    - 단독으로 실행할 수 있는 스프링 애플리케이션을 쉽게 생성
    - Tomcat 같은 웹 서버를 내장해서 별도의 웹 서버를 설치하지 않아도 된다.
    - 손쉬운 빌드 구성을 위한 stater 종속성 제공
    - 스프링과 3rd parth(외부) 라이브러리 자동 구성
    - 메트릭, 상태 확인, 외부 구성 같은 프로덕션 준비 기능 제공
    - 관례에 의한 간결한 설정

## IoC

- Inversion Of Control, 제어의 역전
- 객체의 생성, 생명 주기 관리 등 프로그램의 제어 흐름을 직접 제어하는 것이 아니라, 외부에서 관리하는 것을 말한다.
- 대부분의 프레임워크에서 사용하는 방법으로, 개발자는 프레임워크에 필요한 부분을 개발하고 조립하는 방식의 개발을 하게 된다.

### 프레임 워크 vs 라이브러리

- 프레임워크가 내가 작성한 코드를 제어하고, 대신 실행하면 그것은 프레임 워크가 맞다(JUnit)
- 내가 작성한 코드가 직접 제어의 흐름을 담당한다면 그것은 라이브러리다.

## DI

- Dependency Injection, 의존관계 주입 or 의존성 주입
- 애플리케이션 실행 시점(런타임)에 외부에서 실제 구현 객체를 생성하고 클라이언트에 전달해서 클라이언트와 서버의 실제 의존 관계가 연결 되는 것을 의존관계 주입이라고 한다.
- 의존관계 주입을 사용하면 정적인 클래스 의존관계를 변경하지 않고, 동적인 객체 인스턴스 의존관계를 쉽게 변경할 수 있다.

### 1. 정적인 클래스 의존관계

- 애플리케이션을 실행하지 않아도 import 코드를 보고 분석할 수 있다.
  ![image](https://user-images.githubusercontent.com/87891581/147729405-5b42f0d7-6ffb-4202-ae73-1c450a939542.png)

### 2. 동적인 객체 인스턴스 의존 관계

- 애플리케이션 실행 시점에 실제 생성된 객체 인스턴스의 참조가 연결된 의존관계다.
  ![image](https://user-images.githubusercontent.com/87891581/147729576-56fb37c6-e5d2-4748-8295-f06ad5557f24.png)

## IoC 컨테이너, DI 컨테이너

- 객체를 생성하고 관리하면서 의존관계를 연결해 주는 것을 IoC 컨테이너 또는 DI 컨테이너라고 한다.
- 의존관계 주입에 초점을 맞추어 최근에는 주로 DI 컨테이너라 한다.
- 어셈블러, 오브젝트 팩토리 등으로도 불리기도 한다.

## 스프링 컨테이너

- `ApplicationContext` 인터페이스를 구현한 객체를 스프링 컨테이너라고 부른다.
- 스프링 컨테이너는 XML, 자바 코드 등 다양한 형식의 설정 정보로 만들 수 있다. `BeanDefinition`이라는 빈 설정 메타 정보에 의존하기 때문에 가능하다.
    - 스프링 컨테이너는 설정 형식에 맞는 Reader로 설정 정보를 읽고 `BeanDefinition`을 생성한다.
    - 원하는 형식에 맞는 Reader를 만들어서 `BeanDefinion`을 생성할 수 도 있다.
- `ApplicationContext` 인터페이스는 `BeanFactory` 인터페이스를 상속한 서브 인터페이스다.
- 빈의 관리와 조회를 위한 `BeanFactory`에 편리한 부가 기능을 추가한 것을 `ApplicationContext`라고 부른다.
    - 부가 기능에는 메시지소스를 활용한 국제화 기능(국가에 맞게 언어 변환), 환경 변수 기능, 리소스를 편리하게 조회하는 기능 등이 있다.

## 싱글톤 컨테이너

### 1. 스프링 컨테이너와 싱글톤

- 대부분의 스프링 애플리케이션은 웹 애플리케이션이다. 웹 애플리케이션은 보통 여러 고객이 동시에 요청을 한다.
- 요청할 때 마다 새로운 객체를 생성한다면, 메모리 낭비가 심하다. 이에 대한 해결 방안으로 스프링 컨테이너는 객체를 싱글톤으로 생성하고 관리한다.
    - 싱글톤 패턴이랑 클래스의 인스턴스가 1개만 생성되는 것을 보장하는 디자인 패턴이다.
    - 스프링의 기본 빈 등록 방식은 싱글톤이지만, 싱글톤 방식만 지원하는 것은 아니다.

### 2. 싱글톤 방식의 주의점

- 여러 클라이언트가 하나의 객체 인스턴스를 공유하기 때문에 싱글톤 객체는 무상태로 설계해야 한다.
    - 특정 클라이언트에 의존적인 필드가 있으면 안된다.
    - 특정 클라이언트가 값을 변경할 수 있는 필드가 있으면 안된다.
    - 가급적 읽기만 가능해야 한다.
    - 필드 대신에 자바에서 공유되지 않는 지역변수, 파라미터, ThreadLocal 등을 사용해야 한다.

### 3. `@Configuration`과 싱글톤

- 애노테이션 기반의 스프링 컨테이너의 경우, `CGLIB`라는 클래스의 바이트코드를 조작하는 라이브러리를 사용하여 싱글톤을 유지한다.
- 객체 생성을 담당하는 클래스에 `@Configuration`을 적용한다면, `@Bean`이 붙은 메서드마다 이미 스프링 빈이 존재하면 존재하는 빈을 반환하고, 스프링 빈이 없으면 생성해서 스프링 빈으로 등록하고
  반환하는 코드가 동적으로 만들어진다.
    - `@Bean`만 적용하면 스프링 빈으로 동륵은 되지만, 싱글톤을 보장하지는 않는다.

## 컴포넌트 스캔

- 자바 코드의 `@Bean`이나 XML의 `<bean>` 등을 통해 설정 정보에 스프링 빈을 수동으로 입력할 수 있다.
- 컴포넌트 스캔을 이용하면 설정 정보가 없어도 자동으로 스프링 빈을 등록할 수 있다.
- `@SpringBootApplication`에 `@ComponentScan`이 들어있다.

### 1. 등록 과정

1. `@ComponentScan`이 `@Component`가 붙은 모든 클래스를 스프링 빈으로 등록한다.
    - 이때, 스프링 빈의 기본 이름은 클래스명을 사용하되 맨 앞글자만 소문자를 사용한다.
    - 필요하다면 빈 이름을 직접 지정할 수 있지만, 권장하지는 않는다.
2. 생성자에 `@Autowired`를 지정하면, 스프링 컨테이너가 자동으로 해당 스프링 빈을 찾아서 주입한다.
    - 이때 기본 조회 전략은 타입이 같은 빈을 찾아서 주입한다.

### 2. 탐색 위치

- 기본적으로 `@ComponentScan`이 붙은 설정 정보 클래스의 패키지가 시작 위치가 된다. 하위 패키지까지 모두 탐색한다.
    - 설정 정보 클래스의 위치를 프로젝트 최상단에 두고, 패키지 위치는 지정하지 않는 방법이 권장된다.
- `basePackages`로 탐색할 패키지의 시작 위치를 지정할 수 있다. 여러 시작 위치를 지정할 수 있다.
- `basePackageClasses`로 지정한 클래스의 패키지를 탐색 시작 위치로 지정할 수 있다.

### 3. 컴포넌트 스캔 기본 대상

컴포넌트 스캔은 `@Component`뿐만 아니라 다른 대상도 스캔한다. 엄밀히 말하면, 다른 어노테이션에 `@Component`가 붙어있다.

- @Component : 기본 스캔 대상
- @Controller : 스프링 MVC 컨트롤러로 인식
- @Service : 특별한 기능은 없으며, 핵심 비즈니스 로직이 존재함을 알리기 위해 사용한다.
- @Repository : 스프링 데이터 접근 계층으로 인식하고, 데이터 계층의 예외를 스프링 예외로 변환해준다.
- @Configuration : 스프링 설정 정보에서 사용한다.

### 4. 필터

컴포넌트 스캔 대상을 추가하거나 제외할 수 있다.

- `includeFilters` : 컨포넌트 스캔 대상을 추가로 지정한다. `@Component`면 충분하기 때문에 거의 사용하지 않는다.
- `excludefilters` : 컴포넌트 스캔에서 제외할 대상을 지정한다. 간혹 사용할 때가 있지만 많지는 않다.

#### FilterType 옵선

- ANNOTATION : 기본값. 애노테이션을 인식해서 동작한다.
- ASSIGNABLE_TYPE : 지정한 타입과 자식 타입을 인식해서 동작한다.
- ASPECT_J : AspectJ 패턴 사용
- REGEX : 정규 표현식
- CUSTOM : TypeFilter 이라는 인터페이스를 구현해서 처리

### 5. 중복 등록과 충돌

#### 1) 자동 빈 간에 빈 이름이 중복되는 경우

- 스프링이 `ConflictingBeanDefinitionException` 예외를 발생시킨다.

#### 2) 수동 빈과 자동 빈 간에 빈 이름이 중복되는 경우

- 수동 빈이 자동 빈을 덮어쓴다.
- 대부분 해당 경우가 의도적으로 발생하지 않기 때문에 최근 스프링 부트에서는 오류가 발생하도록 기본 값을 바꾸었다.


## 의존 관계 자동 주입
### 다양한 의존 관계 주입 방법
- 의존 관계 주입은 크게 4가지 방법이 있다.
  - 생성자 주입 : 객체를 생성할 때 딱 1번만 호출되므로, 불변하게 설계할 수 있다. 인자를 누락하거나 final 키워드와 같이 사용하여 값이 설정되지 않는 오류를 컴파일 시점에 막을 수 있다. 이런 이유로 인해 권장되는 방법이다.
  - 수정자 주입 : 변경 가능성이 있는 의존관계에 사용된다.
  - 필드 주입 : 간결하지만, 외부에서 변경이 불가능해서 테스트 하기 힘들다는 단점으로 인해 사용하지 않는다.
    - 테스트 코드나 설정을 목적으로 하는 `@Configuration` 같은 곳에서만 예외적으로 사용한다.
  - 메서드 주입 : 한번에 여러 필드를 주입받을 수 있다. 일반적으로 사용하지 않는다.
- 롬복을 사용하면, 편리하게 개발할 수 있다.

### 주입할 스프링 빈이 없어도 동작해야 하는 경우
- `@Autowired(required=false)` : 자동 주입할 대상이 없으면 메서드 자체가 호출이 안된다.
- `org.springframework.lang.@Nullable` : 자동 주입할 대상이 없으면 null이 입력된다.
- `Optional<>` : 자동 주입할 대상이 없으면 Optional.empty가 입력된다.

### 조회 빈이 2개 이상인 경우
- `@Autowired`는 타입으로 조회하기 때문에 선택된 빈이 2개 이상이면 문제가 발생한다.
  - `NoUniqueBeanDefinitionException` 예외가 발생한다.

#### 해결 방법
1. `@Autowired` 필드 명 매칭
   - `@Autowired`는 먼저 타입 매칭을 시도하고, 여러 빈이 있으면 필드 이름, 파라미터 이름으로 빈 이름을 추가 매칭한다.

2. `@Qualifier`끼리 매칭
   - 빈 이름을 변경하지 않고, 추가 구분자를 붙여주는 방법이다.
   - `@Qualifier`가 매칭되는 `@Qualifier`를 찾지 못한다면, 같은 이름을 가진 스프링 빈을 추가로 찾는다.
     - 매칭 되도록 사용하는 것이 좋다.
   - `@Qualifier`를 갖는 애노테이션을 정의하여 편리하게 사용할 수도 있다.
3. `@Primary` 사용
   - `@Autowired`시 여러 빈이 매칭되면 `@Primary`가 우선권을 가진다.

#### @Primary, @Qualifier 활용 방법
- 주로 사용하는 스프링 빈에 `@Primary`를 적용하고, 종종 사용하는 스프링 빈에 `@Qualifier`을 적용하면 코드를 깔끔하게 유지할 수 있다.
- 우선순위는 `@Qualifier`가 더 높다.
  - 스프링은 자동보다는 수동이, 넓은 범위의 선택권 보다는 좁은 범위의 선택권이 우선순위가 높다.

### 조회한 빈이 모두 필요한 경우 - List, Map
- Map이나 List를 사용하면 스프링이 해당 타입에 맞게 조회한 스프링 빈을 담아서 반환한다.
- 해당하는 타입의 스프링 빈이 없다면 빈 컬렉션이나 Map을 주입한다.

### 자동, 수동의 올바른 실무 기준

> 스프링과 스프링 부트가 자동으로 등록하는 수많은 빈들은 예외다. 메뉴얼을 참고해서 스프링 부트가 의도한 대로 편리하게 사용한다.

- 컨트롤러, 서비스, 리포지토리의 경우 자동 기능을 기본으로 사용한다.
  - 숫자가 매우 많다.
  - 문제 발생 시 어떤 곳에서 문제가 발생했는지 명확하게 파악하기 쉽다.
- 비즈니스 로직 중 다형성을 적극 활용하는 경우에는 수동으로 빈을 등록하거나, 자동으로 하면 특정 패키지에 같이 묶어둔다.
- 기술적인 문제나 공통 관심사(AOP)를 처리하는 경우 수동으로 등록한다.
  - 업무 로직에 비해 그 수가 매우 적다.
  - 애플리케이션 전반에 걸쳐 광범위하게 영향을 미치며, 문제 발생 시 파악하기 어렵다.
