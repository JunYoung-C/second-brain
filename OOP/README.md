# OOP

## 목차

- [좋은 객체 지향 설계의 5가지 원칙(SOLID)](#좋은-객체-지향-설계의-5가지-원칙solid)
- [객체 지향 프로그래밍](#객체-지향-프로그래밍)

---

## 좋은 객체 지향 설계의 5가지 원칙(SOLID)

1. SRP(Single Responsibility Principle) : 단일 책임 원칙
    - 한 클래스는 하나의 책임만 가져야 하며, 클래스를 변경하는 이유는 단 하나의 이유여야 한다.
2. OCP(Open/Closed Principle) : 개방-폐쇄 원칙
    - 소프트웨어의 요소는 확장에는 열려있으나 변경에는 닫혀 있어야 한다.
    - 요구 사항의 변경이나 추가 사항이 발생하더라도, 기존 구성 요소에는 수정이 일어나지 않고, 기존 구성 요소를 쉽게 확장해서 재사용한다.
3. LSP(Liskov Substitution Principle) : 리스코프 치환 원칙
    - 상위 타입의 객체를 하위 타입의 객체로 치환해도 상위 타입을 사용하는 프로그램은 정상적으로 동작해야 한다.
4. ISP(Interface segregation Principle) : 인터페이스 분리 원칙
    - 인터페이스는 그 인터페이스를 사용하는 클라이언트를 기준으로 분리해야 한다.
    - SRP가 클래스의 단일 책임이라면, ISP는 인터페이스의 단일 책임이다.
5. DIP(Dependency Inversion Principle) : 의존관계 역전 원칙
    - 상위 모델은 하위 모델에 의존하면 안된다.
    - 구체화에 의존하면 안되며, 추상화에 의존해야 한다.

## 객체 지향 프로그래밍

### 1. 정의

- 객체 지향 프로그래밍은 컴퓨터 프로그램을 명령어의 목록으로 보는 시각에서 벗어나 여러개의 독립된 단위, 즉 **객체들의 모임**으로 파악하고자 하는 것이다. 각각의 **객체**는 **메시지**를 주고받고, 데이터를 처리할 수 있다(**협력**)
- 객체 지향 프로그래밍은 프로그램을 **유연**하고 **변경**이 용이하게 만들기 때문에 대규모 소프트웨어 개발에 많이 사용된다.

### 2. 특징

1. 추상화 : 객체들의 공통적인 속성이나 기능을 도출하는 것을 말한다.
2. 캡슐화 : 실제로 구현되는 부분을 외부에 드러나지 않도록 하여 정보를 은닉하는 것을 말한다.
3. 상속 : 부모 클래스의 속성과 기능을 그대로 이어받아 사용할 수 있게 하고 기능의 일부분을 변경해야 할 경우 상속받은 자식 클래스에서 해당 기능만 재정의하여 사용할 수 있게 하는 것이다.
4. **다형성** : 프로그램 언어의 각 요소들이 다양한 형태를 가질 수 있는 것을 의미한다. 부모 클래스 타입의 참조 변수로 자식 클래스 타입의 인스턴스를 참조하는 경우나 오버로딩, 오버라이딩이 해당된다.