# Database

<details>
   <summary>DB</summary>

<br/>

- 일정한 규칙, 혹은 규약을 통해 구조화되어 저장되는 데이터의 모음이다.

---

</details>

<details>
   <summary>DB(or DBMS)를 사용하는 이유</summary>

<br/>

- 파일 시스템의 데이터 종속과 중복, 비일관성, 데이터 무결성 등의 문제를 해결하기 위해 사용한다.
  - 데이터 종속 : 파일 시스템에서는 데이터 정의를 응용 프로그램에서 한다. 이러한 의존관계로 인해 데이터 구조를 변경하려면 프로그램을 수정해야 한다.
  - 데이터 중복 : 응용 프로그램별로 독립적인 파일 관리로 인해 데이터의 중복 저장이 발생할 수 있다.
  - 데이터의 비일관성 : 중복 저장된 데이터 중 하나의 데이터만 변경되어 불일치성이 발생할 수 있다.

---

</details>

<details>
   <summary>DBMS</summary>

<br/>

- DataBase Management System. 
- 데이터베이스 관리 시스템으로, 다수의 사용자가 데이터베이스에 접근할 수 있도록 설계된 시스템이다.

---

</details>

<details>
   <summary>SQL</summary>

<br/>

- 데이터 베이스 시스템에서 사용하는 전용 언어이다.
- 데이터 정의어, 데이터 조작어, 데이터 제어어로 구성된다.
  - 데이터 정의어(DDL, Data Definition Language)
    - `CREATE, ALTER, DROP`문과 같이 테이블의 구조를 정의한다.
  - 데이터 조작어(DML, Data Manipulation Language)
    - `SELECT, INSERT, UPDATE, DELETE`문과 같이 데이터 검색, 삽입, 수정, 삭제하는 데 사용한다.
  - 데이터 제어어(DCL, Data Control Language)
    - `GRANT, REVOKE`문과 같이 데이터의 사용 권한을 관리한다.

---

</details>

<details>
   <summary>View</summary>

<br/>

- 하나 이상의 테이블에서 유도된 가상의 테이블이다.
  - 실제 데이터를 디스크에 저장하지 않고, 원본 테이블에서 가져온다.
- 매번 조인할 필요없이 편리하게 사용할 수 있고, 보안이 필요한 속성을 제외하여 정의할 수 있다는 장점이 있다.

---

</details>

<details>
   <summary>스키마</summary>

<br/>

- 데이터베이스의 구조와 제약 조건에 관한 전반적인 명세를 기술한 메타데이터의 집합이다.
- 사용자의 관점에 따라 외부 스키마, 개념 스키마, 내부 스키마로 나눠진다.
  - 외부 스키마 : 전체 데이터베이스 중에서, 사용자나 응용 프로그래머가 필요로 하는 논리적인 부분을 의미한다.
    - ex) 가령 대학교라는 큰 데이터베이스에서, 학생이 필요로 하는 데이터와 교수가 필요로 하는 데이터는 서로 다를 것이다. 각각 필요로 하는 데이터베이스의 일부분이 외부 스키마이다.
  - 개념 스키마 : 전체 데이터베이스의 정의를 의미한다. 통합 조직별로 하나만 존재한다.
  - 내부 스키마 : 물리적 저장 장치에 데이터베이스가 실제로 저장되는 방법의 표현이다.
    ![image](https://user-images.githubusercontent.com/87891581/189832626-44d75403-400e-493a-9d0b-e4d94668fcc9.png)

---

</details>

<details>
   <summary>릴레이션</summary>

<br/>

- 관계형 데이터베이스에서 정보를 구분하여 저장하는 기본 단위이다. 테이블이라고도 부른다.
  - NoSQL 데이터베이스에서는 컬렉션이라고 한다.

---

</details>

<details>
   <summary>엔티티</summary>

<br/>

- 사람, 장소, 물건, 사건, 개념 등 여러 개의 속성을 지닌 명사를 의미한다.
  - 자동차라는 엔티티는 차 번호, 바퀴 수, 색깔, 차종 등 다양한 속성을 가진다.

---

</details>

<details>
   <summary>속성</summary>

<br/>

- 릴레이션에서 관리하는 구체적이며 고유한 이름을 갖는 정보이다.
  - 필드나 열이라고도 부른다.
- 가령 자동차라는 엔티티는 차 번호, 바퀴 수, 색깔, 차종 등 다양한 속성을 가진다. 이때 서비스에서 필요로 하는 엔티티의 속성을 말한다. 
- 한 릴레이션 안에 있는 애트리뷰트 수를 차수(degree)라고 한다.

---

</details>

<details>
   <summary>도메인</summary>

<br/>

- 릴레이션에 포함된 각각의 속성들이 가질 수 있는 값의 집합을 말한다.
  - 성별이라는 속성의 경우 남자와 여자라는 도메인을 가진다.

---

</details>

<details>
   <summary>레코드</summary>

<br/>

- 테이블에 쌓이는 행단위의 데이터를 레코드라고 한다.
  - 튜플이라고도 한다.
- 릴레이션 튜플의 개수를 카디날리티라고 한다.

---

</details>

<details>
   <summary>키</summary>

<br/>

![image](https://user-images.githubusercontent.com/87891581/189832478-685f412c-c269-43bc-94aa-abc25beee439.png)
- 특정 튜플을 식별할 때 사용하는 속성 혹은 속성의 집합이다.
- 종류로는 슈퍼키, 후보키, 기본키, 대체키가 있다.
- 유일성 : 키의 값들이 서로 중복되지 않음.
- 최소성 : 키가 식별할 수 있는 최소한의 속성들로 구성됨.

---

</details>

<details>
   <summary>슈퍼키</summary>

<br/>

- 튜플을 유일하게 식별하는 속성 혹은 속성의 집합이다.
  - 유일성을 만족하는 키다.

---

</details>

<details>
   <summary>후보키</summary>

<br/>

- 튜플을 유일하게 식별할 수 있는 속성의 최소 집합이다.
- 유일성과 최소성을 만족하는 키다.

---

</details>

<details>
   <summary>기본키</summary>

<br/>

- 여러 후보키 중에서 하나를 선택하여 대표로 선정된 키를 말한다.
- 변경의 여지가 있는 자연키보다는, 인위적으로 기본키를 만들어 사용하는 것을 권장한다.
  - 자연키 : 주민번호와 같이 테이블을 생성하면서 자연스레 존재하는 속성인 기본키를 말한다. 

---

</details>

<details>
   <summary>대체키</summary>

<br/>

- 기본키로 선정되지 않은 후보키를 말한다.

---

</details>

<details>
   <summary>외래키</summary>

<br/>

- 다른 릴레이션의 기본키를 참조하는 속성을 말한다. 
- 기본키와 달리 NULL값과 중복값을 허용한다.

---

</details>

<details>
   <summary>ERD</summary>

<br/>

- Entity Relationship Diagram
- 데이터베이스를 구축할 때 가장 기초적인 뼈대 역할을 하며, 릴레이션 간의 관계를 정의한 것을 말한다.

---

</details>

<details>
   <summary>이상현상</summary>

<br/>

- 잘못 설계된 테이블로 삽입, 삭제, 수정 같은 데이터 조작을 할 때 의도와 다르게 동작하는 현상을 말한다.
- 삽입 이상 : 튜플 삽입 시 특정 속성에 해당하는 값이 없어 NULL 값을 입력해야 하는 경우
- 삭제 이상 : 튜플 삭제 시 같이 저장된 다른 정보까지 삭제되는 경우
- 수정 이상 : 튜플 수정 시 중복으로 저장된 데이터 일부만 수정되어 데이터가 일치하지 않는 경우

---

</details>

<details>
   <summary>함수 종속성</summary>

<br/>

- 릴레이션 속성간에 함수적으로 종속하는 성질을 함수 종속성이라고 한다.
  - 어떤 릴레이션에 속하는 속성의 집합 A와 B가 있을 때, A의 값을 알면 B의 값이 유일하게 정해지는 의존 관계를 `Y는 X에 함수 종속`이라고 표현한다.
    - `A -> B`로 표기한다.
    - 이때 A를 결정자라고 하고, B를 종속자라고 한다.

---

</details>

<details>
   <summary>정규화</summary>

<br/>

- 이상현상을 없애기 위해 릴레이션을 분리하는 작업을 말한다.
- 정규화된 정도에 따라 제1정규형, 제2정규형, 제3정규형, 보이스/코드 정규형으로 구분된다.
  - 제1정규형 : 릴레이션의 모든 속성값이 원자값을 가지는 경우
    - ex) A의 취미 속성값이 영화와 음악인 경우, 한 튜플에 (영화, 음악)을 넣으면 이는 원자값이 아니다.
  - 제2정규형 : 릴레이션이 제1정규형이고, 모든 비주요 속성이 후보키에 완전 함수 종속인 경우 
    - 완전 함수 종속 : 어떤 릴레이션에 속하는 속성의 집합 A와 B가 있을 때, B가 A 속성 전체에 함수 종속이고 B가 A의 부분집합 속성에 함수 종속이 아닌 경우를 말한다.
    - 비주요 속성 : 후보키에 속하지 않는 속성 
  - 제3정규형 : 릴레이션이 제2정규형이고, 모든 비주요 속성이 후보키에 이행적 종속 상태가 아닌 경우
    - 이행적 종속 : B가 A에 함수 종속이고 C가 B에 함수 종속일 때, C가 A에 이행적 함수 종속 상태라고 말한다.
  - 보이스/코드 정규형(BCNF) : 릴레이션이 제3정규형이고, 모든 결정자가 후보키인 경우를 말한다.
    - ex) 복합키 (A, B)가 C의 결정자이고 C가 B의 결정자인 경우 BCNF를 만족하지 않는다.

---

</details>

<details>
   <summary>반정규화(비정규화)</summary>

<br/>

- 조인으로 인한 성능 저하와 같은 이유로, 조회 성능 향상을 위해 정규화를 되돌리는 것을 말한다.

---

</details>

<details>
   <summary>트랜잭션</summary>

<br/>

- 데이터베이스에서 하나의 논리적 기능을 수행하기 위한 작업의 단위를 말한다.
  - `A 계좌에서 B계좌로 만원을 이체한다.`라는 요구사항을 하나의 논리적인 기능으로 볼 수 있다. 기능 구현을 위해 `A 계좌에서 만원을 인출하는 UPDATE문`과 `B 계좌로 만원을 입금하는 UPDATE문` 이라는 작업을 필요로 한다.

---

</details>

<details>
   <summary>트랜잭션 특징</summary>

<br/>

- 원자성(Atomicity)
  - 트랜잭션에 포함된 작업은 전부 수행되거나 아니면 전부 수행되지 않아야 한다.

- 일관성(Consistency)
  - 트랜잭션을 수행하기 전이나 수행한 후나 데이터베이스는 항상 일관된 상태를 유지해야 한다.
    - 데이터베이스는 트랜잭션 수행 전이나 후 모두 정해진 제약이나 규칙을 만족해야 한다는 뜻이다.

- 고립성(Isolation)
  - 여러 트랜잭션이 동시에 수행될 때 각 트랜잭션은 상호 간섭 없이 독립적으로 수행된다.

- 지속성(Durability)
  - 트랜잭션이 성공적으로 수행되면, 데이터베이스에 작업의 결과가 영구적으로 저장되어야 한다.
    - 트랜잭션 수행 중에 오류가 발생하더라도 로그 파일을 이용하여 트랜잭션 이전으로 돌아갈 수 있다.

---

</details>

<details>
   <summary>트랜잭션 상태</summary>

<br/>

![image](https://user-images.githubusercontent.com/87891581/190902409-ffc86a1c-3d41-4888-876a-6ed64b141880.png)
- 활성화(Active)
  - 트랜잭션이 실행중인 상태
- 실패(Failed)
  - 트랜잭션에 오류가 발생하여 실행이 중단된 상태
- 철회(Aborted)
  - 트랜잭션이 비정상적으로 종료되어 Rollback 연산을 수행한 상태
- 부분 완료(Partially Committed)
  - 트랜잭션 수행이 완료되어 commit 요청이 들어온 직후의 상태. 
  - 트랜잭션 결과가 db에 반영되지 않음.
- 완료(Committed)
  - commit 요청이 처리되어 트랜잭션이 성공적으로 종료된 상태.
  - 트랜잭션 결과가 db에 반영됨.

---

</details>

<details>
   <summary>트랜잭션 격리 수준의 필요성</summary>

<br/>

- 트랜잭션이 데이터를 다루고 있는 경우 다른 트랜잭션이 접근하지 못하도록 막는 것이 필요하다. 하지만 모든 경우에 락을 사용하여 순서대로 처리하도록 하면 DB 성능이 떨어지게 된다. 
  - 트랜잭션이 동시 접근 시 가능한 경우
    1. 읽기 작업을 하는 트랜잭션 간에 동시 접근을 허용하더라도 문제가 발생하지 않는다.
    2. 쓰기 작업을 하는 트랜잭션 간에 동시 접근을 허용하면 갱신 손실이 발생하므로 락을 사용해야한다.
    3. 읽기 작업을 하는 트랜잭션과 쓰기 작업을 하는 트랜잭션 간에는 더티 리드, 반복 불가능한 리드, 팬텀 리드 문제가 발생할 수 있다.

---

</details>

<details>
   <summary>트랜잭션 격리 수준</summary>

<br/>

- Read Uncommitted
  - 다른 트랜잭션이 커밋하지 않은 데이터를 읽을 수 있는 격리 수준이다. (Dirty Read) 
  - SELECT를 수행하는 동안 해당 데이터에 공유락을 걸지 않는다.
    - UPDATE시 베타락은 기본적으로 건다.
  - 다른 트랜잭션에 공유락과 베타락이 걸린 데이터를 대기하지 않고 읽는다.
- Read Committed
  - 커밋 완료된 데이터만 읽을 수 있는 격리 수준이다.
  - 어떤 트랜잭션이 접근한 행을 다른 트랜잭션이 수정할 수 있기 때문에 조회 결과가 비일관적일 수 있다. (Non-Repeatable Read)
  - SELECT를 수행하는 동안 해당 데이터에 공유락을 걸지만, 수행 직후 해지한다. 즉, 트랜잭션 실행 중간에 해지될 수 있다. 
- Repeatable Read
  - 하나의 트랜잭션이 접근한 데이터를 다른 트랜잭션이 수정할 수 없도록 막아주지만, 새로운 행이 추가되는 것을 막지 않는 격리수준이다. (Phantom Read)
  - SELECT를 수행하는 동안 해당 데이터에 공유락을 걸고, 트랜잭션을 종료할 때까지 유지한다.
- Serializable
  - 하나의 트랜잭션이 접근한 데이터에 다른 트랜잭션이 접근할 수 없는 격리수준이다.
  - SELECT를 수행하는 동안 해당 데이터에 공유락을 걸고, 트랜잭션을 종료할 때까지 유지한다.

---

</details>

<details>
   <summary>격리 수준에 따라 발생하는 현상</summary>

<br/>

- Dirty Read
  - 커밋되지 않은 수정 중인 데이터를 다른 트랜잭션에서 읽을 수 있을 때 발생하는 현상을 말한다.
  - 수정중인 데이터가 롤백되더라도 다른 트랜잭션에서는 롤백되지 않은 데이터로 작업이 진행된다.
  - 발생 Level : Read Uncommitted
- Non-Repeatable Read
  - 한 트랜잭션이 읽기 작업을 반복할 경우 이전의 결과가 반복되지 않는 현상을 말한다.
  - 발생 Level : Read Uncommitted, Read committed
- Phantom Read
  - 한 트랜잭션이 읽기 작업을 반복할 경우 이전에 없던 데이터(유령 데이터)가 나타나는 현상을 말한다.
  - 발생 Level : Read Uncommitted, Read committed, Repeatable Read

---

</details>

<details>
   <summary>Commit</summary>

<br/>

- 트랜잭션을 종료하기 위해 사용하는 명령어

---

</details>

<details>
   <summary>Rollback</summary>

<br/>

- 트랜잭션이 수행한 결과를 원래의 상태로 되돌리는 명령어

---

</details>

<details>
   <summary>동시성 제어</summary>

<br/>

- 트랜잭션이 동시에 수행될 때, 일관성을 해치지 않도록 트랜잭션의 데이터 접근을 제어하는 것

---

</details>

<details>
   <summary>갱신 손실 문제</summary>

<br/>

- 여러 개의 트랜잭션이 한 개의 데이터를 동시에 갱신할 때 어떤 트랜잭션의 갱신이 무효화되는 문제를 말한다.

---

</details>

<details>
   <summary>락</summary>

<br/>

- 한 트랜잭션이 데이터를 읽거나 수정할 때 다른 트랜잭션의 접근을 막는 기능이다.
- 락을 해지(언락)해야 다른 트랜잭션이 해당 데이터에 접근할 수 있다.

---

</details>

<details>
   <summary>락의 유형</summary>

<br/>

- 공유락
  - 읽기를 할 때 사용하는 락을 말한다.
  - 여러 트랜잭션이 동시에 데이터를 읽어도 변경되지 않기 때문에, 공유락이 걸린 데이터에 공유락 요청을 허용한다.
- 베타락
  - 쓰기를 할 때 사용하는 락을 말한다.
  - 베타락이 걸린 데이터에는 공유락과 베타락 요청 모두 허용하지 않는다.

---

</details>

