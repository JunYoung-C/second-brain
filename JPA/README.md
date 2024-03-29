# JPA

<details>
   <summary>영속성</summary>

<br/>

- 데이터를 생성한 프로그램의 실행이 종료되더라도 사라지지 않는 데이터의 특성
- 데이터를 파일이나 DB에 저장함으로써 데이터에 영속성을 부여한다.

---

</details>

<details>
   <summary>JDBC</summary>

<br/>

- 자바에서 데이터베이스에 접속할 수 있도록 하는 자바 API이다.
- JDBC API를 이용하여 DBMS의 종류와 상관없이 DB 작업을 처리할 수 있다.
  - 각각의 DBMS를 이를 구현한 JDBC Driver가 존재한다.

---

</details>

<details>
   <summary>Spring JDBC</summary>

<br/>

- JDBC의 저수준 처리를 스프링 프레임워크에 위임하여, Connection 연결 객체 생성 및 종료, Statement 준비/실행 및 종료 등의 반복되는 처리를 대신해준다.

---

</details>

<details>
   <summary>MyBatis</summary>

<br/>

- 반복적인 JDBC 프로그래밍을 단순화하고, 코드에서 SQL을 분리하는 목적을 가진 프레임워크
- 객체와 SQL을 매핑하는 방식
- 물리적으로 코드와 SQL을 분리했더라도 논리적으로는 강한 의존성을 가지고 있다.
    - 특정 DB에 종속
    - 테이블마다 비슷한 CRUD 작업이 반복적이다.
    - 테이블 필드 변경 시 이와 관련된 모든 DAO의 SQL문과 객체의 필드 등을 수정해야 한다.
    - SQL 중심의 개발

---

</details>

<details>
   <summary>ORM</summary>

<br/>

- Object Relational Mapping
- 객체와 관계형 데이터베이스의 테이블을 매핑하여 데이터를 객체화하는 기술이다.
- 객체는 객체대로 설계하고 관계형 데이터베이스는 관계형 데이터베이스대로 설계하더라도, ORM 프레임워크가 자바 객체와 관계형 DB를 매핑해준다.
  - 특정 데이터베이스에 의존적이지 않다.

---

</details>

<details>
   <summary>JPA</summary>

<br/>

- Java Persistence API
- 자바 진영의 ORM 기술 표준으로 사용되는 인터페이스 모음이다.
- 대표적인 구현체로 하이버네이트가 있고, SQL 중심의 개발에서 객체 중심의 개발을 할 수 있도록 기능을 제공한다.

---

</details>

<details>
   <summary>Spring Data JPA</summary>

<br/>

- JPA를 사용할 때마다 반복적으로 작성하는 코드를 자동화 해준다.
  - `JPARepository`라는 인터페이스를 통해 공통 CRUD 기능 제공
  - 메소드 이름으로 쿼리 생성 기능 제공 등
    - 페치 조인 필요시 `@EntityGraph`와 같이 사용

---

</details>

<details>
   <summary>JPA를 사용하는 이유</summary>

<br/>

- 패러다임 불일치 문제 해결
  - 객체는 추상화, 상속, 다형성이라는 개념이 있고, 연관관계를 참조로 맺는다. 관계형 데이터베이스는 추상화, 상속, 다형성이라는 개념이 없고, 연관관계를 외래키로 맺는다.
  - 이런 패러다임의 불일치 사이에서 데이터를 주고 받으려면 번거로운 변환 작업이 필요하다. 이를 JPA가 해결해준다.
    - ex1) 상속 관계를 표현하기 위해 슈퍼 타입과 서브 타입을 사용하더라도, 데이터 저장 시 쿼리 한번으로 불가하고 조회 시 JOIN을 해야 한다.
    - ex2) 조인해서 조회하는 SQL 작성 -> SQL에 의존적인 클래스 구현하여 데이터를 받아오기 -> 참조 관계를 가지도록 변환
    - ex3) 반환된 엔티티가 다른 엔티티를 참조하는 경우, 연관 엔티티가 정말 들어있는지 신뢰할 수 없다.
    - ex4) 값이 동일하더라도 서로 다른 객체로 인식할 수 있다.
- 생산성 향상
  - 반복적인 CRUD용 SQL을 개발자가 작성하지 않아도 된다.
- 특정 DB에 종속적이지 않음.
- 유지보수 용이
  - 테이블 필드 추가, 삭제 시 CRUD를 수정할 필요 없이 엔티티만 수정해주면 된다.
  
---

</details>

<details>
   <summary>엔티티</summary>

<br/>

## 엔티티
- 데이터베이스 테이블과 ORM 매핑되어 있는 객체이다.
- `@Entity`가 붙은 클래스는 JPA가 관리하며, 엔티티라고 부른다.

### 엔티티의 생명 주기
![image](https://user-images.githubusercontent.com/87891581/168966197-c708e0b4-ca49-4e0c-898b-7d30a478330a.png)
- 비영속(new/transient) : 영속성 컨텍스트와 전혀 관계가 없는 순수한 객체 상태
- 영속(managed) : 영속성 컨텍스트에 의해 관리되는 상태
- 준영속(detached) : 영속 상태의 엔티티가 영속성 컨텍스트에서 분리된 상태
  - 영속 상태가 된적이 있기 때문에 반드시 식별자가 있다.
  - 임의로 만들어낸 엔티티도 기존 식별자를 가지고 있으면 준영속 엔티티로 볼 수 있다.
- 삭제(removed) : 삭제된 상태

---

</details>

<details>
   <summary>준영속 엔티티를 수정하는 2가지 방법</summary>

<br/>

**1. 변경 감지 기능 사용**
- 권장하는 방법
- 영속성 컨텍스트에서 엔티티를 조회한 후에 데이터를 직접 수정하는 방법
- 동작 방식
  1. 트랜잭션 안에서 다시 조회한 엔티티의 값을 변경
  2. 트랜잭션 커밋 시점에 변경 감지(Dirty Checking) 기능이 동작
  3. 데이터베이스에 update SQL 실행

**2. 병합 사용**
![image](https://user-images.githubusercontent.com/87891581/169645596-e958a5dc-d9cd-4f40-85a9-65ca6112bb84.png)
- 준영속 상태의 엔티티를 영속 상태로 변경할 때 사용하는 기능
- 모든 필드를 변경해버리고, 데이터가 없으면 null로 업데이트를 해버린다.
  - 변경 폼 화면에서 모든 데이터를 항상 유지해야 하기 때문에 오히려 번거로워진다.
- 동작 방식
  1. `merge()` 실행
  2. 파라미터로 넘어온 준영속 엔티티의 식별자 값으로 1차 캐시에서 엔티티 조회
     - 식별자 값이 없다면, 새로운 엔티티로 판단해서 영속화한다.
     - 1차 캐시에 엔티티가 없으면, 데이터베이스에서 엔티티를 조회하고 1차 캐시에 저장
  3. 조회한 영속 엔티티의 값을 준영속 엔티티의 값으로 모두 교체
  4. 트랜잭션 커밋 시점에 변경 감지 기능이 동작해서 데이터베이스에 update SQL 실행

---

</details>

<details>
   <summary>영속성 컨텍스트</summary>

<br/>

- 엔티티를 영구 저장하는 환경이라는 뜻이다.
- 엔티티 매니저로 엔티티를 저장하거나 조회하면, 엔티티 매니저는 영속성 컨텍스트에 엔티티를 보관하고 관리한다.

---

</details>

<details>
   <summary>영속성 컨텍스트의 이점</summary>

<br/>

#### 1. 1차 캐시
- `save()`나 `find()`를 호출하면 엔티티가 1차 캐시에 등록된다.
- 1차 캐시에 등록된 엔티티를 조회한다면, 조회 쿼리 없이 1차 캐시에서 바로 조회할 수 있다.
#### 2. 동일성(identity) 보장
- 영속 엔티티는 1차 캐시에서 조회하므로 동일한 참조값의 엔티티를 보장한다.
#### 3. 트랜잭션을 지원하는 쓰기 지연(transactional write-behind)
- 커밋하기 전까지 SQL문을 모아두었다가 한번에 전송할 수 있다.
#### 4. 변경 감지(dirty checking)
- 영속 엔티티의 데이터를 수정하고 플러시하면, 자동으로 데이터베이스에 변경 내용이 반영된다.
- 과정
  1. 영속 엔티티의 데이터 수정 후 플러시 발생
  2. 영속성 컨텍스트가 스냅샷과 엔티티를 비교하여 변경을 감지
  3. 쓰기 지연 SQL 저장소에 UPDATE 쿼리 등록
  4. 쓰기 지연 SQL 저장소의 쿼리를 데이터베이스에 전송
#### 5. 지연 로딩(lazy loading)
- 엔티티를 실제 사용하는 시점에 SQL을 날려 데이터를 가져온다. 

---

</details>

<details>
   <summary>플러시</summary>

<br/>

- 영속성 컨텍스트의 변경 내용을 데이터베이스에 반영
  - 영속성 컨텍스트를 비우지 않는다.
- 플러시하는 방법
  - `em.flush()` - 직접 호출
  - 트랜잭션 커밋 - 플러시 자동 호출
  - JPQL 쿼리 실행 - 플러시 자동 호출

---

</details>

<details>
   <summary>연관관계 매핑</summary>

<br/>

- 객체의 참조와 테이블의 외래키를 매핑하는 것을 말한다.
  - 객체는 참조용 필드가 있는 쪽으로만 참조가 가능하다.(단방향)
  - 테이블은 외래키 하나로 양쪽 조인이 가능하다.(양방향)
- 객체는 참조 한번으로 단방향 관계를 맺을 수 있지만, 테이블은 외래키 하나로 양방향 관계를 맺을 수 있다.
- 이때 객체를 양방향 참조 관계로 변경 한다면, 객체의 두 관계 중 한쪽만 외래키를 관리하도록 하고, 다른 한쪽은 읽기만 가능하도록 설정해야 한다.
  - 외래키를 관리하는 참조를 연관관계 주인이라고 말한다.
  - 연관관계 주인에는 `@JoinColumn`을 붙여 외래키를 매핑해주고, 반대편에는 `mappedBy` 속성으로 주인을 지정해준다.

---

</details>

<details>
   <summary>다대다 매핑</summary>

<br/>

관계형 데이터베이스에서는 정규화된 테이블 2개로 다대다 관계를 표현할 수 없기 때문에, 연결 테이블을 추가해서 일대다, 다대일 관계로 풀어내야한다.

객체에서는 컬렉션을 사용하고 `@JoinTable`로 연결 테이블을 지정하여 다대다 매핑을 할 수 있지만, 연결 테이블에 데이터 추가가 불가능하다는 단점이 있다.
대신, 연결 테이블용 엔티티를 추가하여 사용하면, 원하는 컬럼을 자유롭게 추가하며 사용할 수 있다. 

---

</details>

<details>
   <summary>상속관계 매핑</summary>

<br/>

- 객체의 상속 관계를 DB에 매핑
- 부모 클래스에 `@Inheritance`를 붙여서 상속 관계 명시
- 일반적으로 `JOINED` 전략을 사용하고, 단순하면 `SINGLE_TABLE` 전략을 사용한다.
  - 조회 시 조인이 필요 없으므로 쿼리가 단순해지고 성능이 증가하기 떄문이다. 정규화 측면에서는 BAD
  - `TABLE_PER_CLASS` 전략은 부모 테이블이 없기 때문에 자식 테이블을 통합해서 쿼리하기 어렵고 성능도 안좋음
- 부모, 자식 클래스 모두 엔티티

---

</details>

<details>
   <summary>@MappedSuperclass</summary>

<br/>

- 생성 날짜와 같이 객체 간에 공통 매핑 정보가 필요할 때 사용한다.
- 부모 클래스를 상속 받는 자식 클래스에게 매핑 정보만 제공한다.
- 엔티티가 아니므로 테이블과 매핑되지 않는다.
  - 상속 관계 매핑이 아니다.

---

</details>

<details>
   <summary>find() vs getReference()</summary>

<br/>

- `entityManager.find()`
  - 영속성 컨텍스트가 비어있으면, 데이터베이스를 통해 실제 엔티티 객체를 조회
- `entityManager.getReference()`
  - 영속성 컨텍스트가 비어있으면, 프록시 엔티티 객체를 조회. 처음 사용하는 시점에 실제 엔티티 객체를 초기화한 후 접근
  - 프록시 객체는 실제 객체를 상속하여 생성됨
- 두 메소드 모두 영속성 컨텍스트에 찾는 객체가 이미 있다면, 프록시 여부와 상관없이 해당 객체를 조회.
  - 같은 트랜잭션 내에서는 동일 참조 보장

---

</details>

<details>
   <summary>즉시 로딩과 지연 로딩</summary>

<br/>

- 즉시로딩
  - 엔티티를 조회할 때 연관된 엔티티도 함께 조회한다.
  - 연관된 엔티티는 실제 엔티티 객체를 참조한다.
  - 단점
    - 즉시 로딩은 연관 엔티티가 당장 필요하지 않더라도 조회하기 때문에 리소스가 낭비된다.
    - JPQL 조회 시 N+1 문제가 발생할 수 있다.
- 지연로딩
  - 엔티티를 조회할 때 연관된 엔티티는 프록시를 참조하여 조회한다.
  - 연관된 엔티티는 실제 사용하는 시점에 DB에서 조회한다.

---

</details>

<details>
   <summary>일대일 관계에서 지연 로딩 주의점</summary>

<br/>

- 외래키가 있는 테이블에 매핑된 엔티티가 연관관계 주인을 가지고 있다면, 조회 시점에 프록시를 넣을지 null을 넣을지 결정할 수 있다.
- 외래키가 없는 테이블에 매핑된 엔티티가 연관관계 주인을 가지고 있다면, 프록시를 넣을지 null을 넣을지 모르기 때문에 이를 결정하기 위해 즉시 로딩이 발생한다.
  - 클래스는 데이터 없음을 null로 표현하지만, 프록시를 미리 넣으면 null을 넣을 수 없다.
  - 컬렉션은 데이터가 없음을 Empty로 표현할 수 있기 때문에, 동일한 상황의 일다다에서는 지연 로딩이 가능하다.

---

</details>

<details>
   <summary>N+1 문제</summary>

<br/>

- 첫 쿼리와 연관된 엔티티들을 조회하기 위해 추가 쿼리가 발생하는 문제
- 즉시 로딩에서의 N+1 문제
  - 멤버 엔티티가 팀 엔티티를 참조하고 즉시 로딩으로 설정되어 있다고 하자. JPQL로 멤버 엔티티 N개를 조회하면, `N개의 멤버를 조회하는 쿼리 1개` + `각 멤버가 참조하는 팀을 조회하는 쿼리 N개`가 발생한다.
    - JPA 구현체는 가능하면 조인을 사용해서 한번에 조회한다.
    - JPQL은 SQL로 번역되어 조회한 다음, 뒤늦게 즉시 로딩임을 확인하고 추가 쿼리를 발생시킨다.
    - 단, 추가 쿼리 대상이 영속성 컨텍스트에 존재하는 경우 쿼리없이 가져온다.
  - 해결 방안은 지연 로딩을 기본적으로 사용하고, 즉시 로딩이 필요한 경우 페치 조인을 사용한다.
    - `@ManyToOne`과 `@OneToOne`은 기본이 즉시 로딩이므로, LAZY로 설정해야 한다.
    - Spring Data JPA의 `@EntityGraph`으로도 페치 조인을 할 수 있다.
- 지연 로딩에서의 N+1 문제
  -  지연 로딩 전략을 사용한 엔티티나 컬렉션을 실제 사용하는 시점에 추가 쿼리가 실행되기 떄문에 문제가 발생한다. 
  - 해결 방안은 페치 조인과 Batch size가 있다.
    - 페치 조인은 join으로 한번에 가져오는 방식으로, 지연 로딩 전략보다 우선시 된다.
    - 컬렉션의 경우, 페치 조인보다는 Batch size 설정을 통해 In 쿼리로 한번에 가져오도록 한다.
---

</details>

<details>
   <summary>영속성 전이와 고아 객체</summary>

<br/>

### 1. 영속성 전이
- 특정 엔티티를 영속 상태로 만들 때 연관된 엔티티도 함께 영속 상태로 만들고 싶으면 영속성 전이 기능을 사용하면 된다.
  - ex) 부모 엔티티를 저장할 때 자식 엔티티도 함께 저장
- 영속성 전이는 연관관계 매핑과 아무 관련이 없다.

### 2. 고아 객체
- 부모 엔티티에서 참조가 제거된 자식 엔티티를 고아 객체라고 하며, JPA는 고아 객체를 자동으로 삭제하는 기능을 제공한다.
  - 부모를 제거할 때 자식도 함께 제거하는 기능도 제공한다.(= `CascadeType.REMOVE`)
- 참조하는 곳이 하나일 때만 사용해야 한다.
  - ex) 게시판과 첨부파일 관계

### 3. 영속성 전이 + 고아 객체
- `CascadeType.ALL` + `orphanRemoval=true`
- 두 옵션을 모두 활성화하면 부모 엔티티를 통해서 자식의 생명 주기를 관리할 수 있다.

---

</details>

<details>
   <summary>임베디드 타입</summary>

<br/>

- 응집도 높은 필드들을 모아 새로운 타입으로 정의하여 사용할 수 있다.
  - ex) 도시 + 번지 + 우편번호 -> 주소로 묶기
- 해당 타입을 사용하더라도 테이블은 변하지 않는다.
- 해당 임베디드 타입을 소유한 엔티티에 생명 주기를 의존한다.
- 해당 타입을 정의한 곳에 `@Embeddable`을 붙이고, 사용하는 곳에 `@Embedded`를 붙인다. 

---

</details>

<details>
   <summary>JPQL</summary>

<br/>

- JPA를 사용하면 엔티티 객체를 중심을 개발할 수 있다. 하지만 필요한 데이터만 DB에서 불러오기 위해 SQL이 필요한 순간이 있다.
- 이를 위해 JPA는 테이블이 아닌 객체를 대상으로 하는 객체 지향 쿼리 언어를 제공하며, 이를 JPQL이라고 부른다.

**특징**
- 엔티티 객체를 대상으로 쿼리한다.
- JPQL은 SQL을 추상화해서 특정 데이터베이스 SQL에 의존하지 않는다.
- JPA는 JPQL을 분석한 다음 적절한 SQL로 변환한다.
- FROM 절의 서브쿼리는 현재 JPQL에서 불가능하다.
- 연관 관계를 가지는 필드를 참조할 때 묵시적 조인이 발생한다.
  - 파악하기 어렵고, 항상 내부 조인만 발생하므로 가급적 명시적으로 조인을 사용한다.

---

</details>

<details>
   <summary>페치 조인</summary>

<br/>

- 연관된 엔티티나 컬렉션을 한 번에 조회하는 기능이다.
  - 조인의 종류가 아니다.
  - 글로벌 로딩 전략을 지연 로딩으로 하고, 최적화가 필요할 때 페치 조인을 적용한다.
- 컬렉션 페치 조인은 주의해서 사용해야 한다.

---

</details>

<details>
   <summary>컬렉션 페치 조인 주의점</summary>

<br/>

1. 일대다 관계의 컬렉션을 페치 조인 하면, `일`의 row 수가 `다`의 row만큼 증가한다.
   - ex) 멤버 1과 멤버 2가 팀A 소속일 때 팀A를 조회하면, 기대한 1건의 팀A가 아니라 2건의 팀A가 조회된다.
   - JPQL의 `DISTINCT`로 엔티티 중복을 제거할 수 있다.
2. 페이징 쿼리를 적용하면 성능상에 문제가 발생한다.
   - 일대다 페치 조인으로 증가된 상태인 row에 페이징이 적용되지 않도록, 하이버네이트는 모든 row를 메모리에 적재하여 처리한다. 테이블에 100만건의 데이터가 있으면, 모두 가져온 다음에 페이징을 적용한다는 의미이다. 이는 성능에 악영향을 주기 때문에 사용해서는 안된다.
   - 해결 방안으로는, 먼저 컬렉션 페치 조인 없이 페이징 처리만 적용하여 조회한다. 그리고 N+1 문제가 발생하지 않도록 batch size를 설정해주면 된다.
     - 다대일, 일대일 페치 조인은 row수를 증가시키지 않으므로 페이징 쿼리에 영향을 주지 않는다.
     - batch size로 설정한 size만큼 IN 쿼리로 조회한다. 단, dto에는 적용되지 않는다.
3. 둘 이상의 컬렉션 페치 조인을 사용하면 안된다.
   - 데이터 정합성에 문제가 발생할 수 있다.
---

</details>

<details>
   <summary>API 요청 파라미터나 응답 값으로 엔티티 사용 시 문제점</summary>

<br/>

- 문제점
  - 엔티티에 프레젠테이션 계층을 위한 로직이 추가된다.
    - 요청 시 : `@NotEmpty` 등
    - 응답 시 : `@JsonIgnore`, 지연 로딩 처리를 위한 설정 등
  - 엔티티가 변경되면 API 스펙이 변한다.
  - 엔티티 하나로 여러 API 스펙을 맞추기 어렵다.
  - 엔티티로 API 스펙을 유추하기 어렵다.
- 해결 방안
  - API 요청 스펙에 맞는 별도의 DTO를 사용한다.

---

</details>

<details>
   <summary>OSIV</summary>

<br/>

- Open Session In View
  - 현재의 엔티티매니저가 초기에는 `Session`으로 불리던 것이 관례가 되었다.
- 영속성 컨텍스트를 뷰까지 열어두기 때문에 뷰와 컨트롤러에서 지연 로딩을 가능하도록 한다.
  - OSIV를 끄면 트랜잭션이 끝나기 전에 지연 로딩을 강제로 호출해두어야 한다.
- 영속성 컨텍스트를 유지하는 만큼 데이터베이스 커넥션 리소스를 사용하기 때문에, 실시간 트래픽이 중요한 애플리케이션에서는 커넥션이 모자를 수가 있다.
  - ADMIN처럼 커넥션을 많이 사용하지 않는 곳에서는 사용해도 좋다.

---

</details>

<details>
   <summary>쿼리 작성 시 권장하는 방법</summary>

<br/>

1. 메소드 이름으로 쿼리 생성 기능 활용
2. 메소드 이름이 복잡해진다면, `@Query`으로 쿼리를 직접 작성하거나 QueryDsl을 사용한다.

---

</details>

<details>
   <summary>QueryDsl을 사용하는 이유 </summary>

<br/>

- QueryDsl을 사용하면 컴파일 타임에 오류를 잡을 수 있고, 동적 쿼리를 쉽게 작성할 수 있다.
  - where 조건에 null값은 무시되기 때문에 동적 쿼리 쉽게 작성 가능
- DTO를 사용한 쿼리 작성 지원
  - DTO 생성자에 `@QueryProjection`을 붙이면 편리하게 쿼리 작성 가능
- where 조건절을 함수로 추상화하여 재활용할 수 있다.

---

</details>