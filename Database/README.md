# Database
- DB
- DB(or DBMS)를 사용하는 이유
- DBMS
- SQL
- View
- 스키마
- 릴레이션
- 엔티티
- 속성
- 도메인
- 레코드
- 키
- 슈퍼키
- 후보키
- 기본키
- 외래키
- ERD
- 이상현상
- 함수 종속성
- 정규화
- 반정규화

### DB
<details>
   <summary>답안 보기</summary>

- 일정한 규칙, 혹은 규약을 통해 구조화되어 저장되는 데이터의 모음이다.

</details>

---

### DB(or DBMS)를 사용하는 이유
<details>
   <summary>답안 보기</summary>

- 파일 시스템의 데이터 종속과 중복, 비일관성, 데이터 무결성 등의 문제를 해결하기 위해 사용한다.
  - 데이터 종속 : 파일 시스템에서는 데이터 정의를 응용 프로그램에서 한다. 이러한 의존관계로 인해 데이터 구조를 변경하려면 프로그램을 수정해야 한다.
  - 데이터 중복 : 응용 프로그램별로 독립적인 파일 관리로 인해 데이터의 중복 저장이 발생할 수 있다.
  - 데이터의 비일관성 : 중복 저장된 데이터 중 하나의 데이터만 변경되어 불일치성이 발생할 수 있다.

</details>

---

### DBMS
<details>
   <summary>답안 보기</summary>

- DataBase Management System. 
- 데이터베이스 관리 시스템으로, 다수의 사용자가 데이터베이스에 접근할 수 있도록 설계된 시스템이다.

</details>

---

### SQL
<details>
   <summary>답안 보기</summary>

- 데이터 베이스 시스템에서 사용하는 전용 언어이다.
- 데이터 정의어, 데이터 조작어, 데이터 제어어로 구성된다.
  - 데이터 정의어(DDL, Data Definition Language)
    - `CREATE, ALTER, DROP`문과 같이 테이블의 구조를 정의한다.
  - 데이터 조작어(DML, Data Manipulation Language)
    - `SELECT, INSERT, UPDATE, DELETE`문과 같이 데이터 검색, 삽입, 수정, 삭제하는 데 사용한다.
  - 데이터 제어어(DCL, Data Control Language)
    - `GRANT, REVOKE`문과 같이 데이터의 사용 권한을 관리한다.

</details>

---

### View
<details>
   <summary>답안 보기</summary>

- 하나 이상의 테이블에서 유도된 가상의 테이블이다.
  - 실제 데이터를 디스크에 저장하지 않고, 원본 테이블에서 가져온다.
- 매번 조인할 필요없이 편리하게 사용할 수 있고, 보안이 필요한 속성을 제외하여 정의할 수 있다는 장점이 있다.

</details>

---

### 스키마
<details>
   <summary>답안 보기</summary>

- 데이터베이스의 구조와 제약 조건에 관한 전반적인 명세를 기술한 메타데이터의 집합이다.
- 사용자의 관점에 따라 외부 스키마, 개념 스키마, 내부 스키마로 나눠진다.
  - 외부 스키마 : 전체 데이터베이스 중에서, 사용자나 응용 프로그래머가 필요로 하는 논리적인 부분을 의미한다.
    - ex) 가령 대학교라는 큰 데이터베이스에서, 학생이 필요로 하는 데이터와 교수가 필요로 하는 데이터는 서로 다를 것이다. 각각 필요로 하는 데이터베이스의 일부분이 외부 스키마이다.
  - 개념 스키마 : 전체 데이터베이스의 정의를 의미한다. 통합 조직별로 하나만 존재한다.
  - 내부 스키마 : 물리적 저장 장치에 데이터베이스가 실제로 저장되는 방법의 표현이다.
    ![image](https://user-images.githubusercontent.com/87891581/189832626-44d75403-400e-493a-9d0b-e4d94668fcc9.png)
</details>

---

### 릴레이션
<details>
   <summary>답안 보기</summary>

- 관계형 데이터베이스에서 정보를 구분하여 저장하는 기본 단위이다. 테이블이라고도 부른다.
  - NoSQL 데이터베이스에서는 컬렉션이라고 한다.

</details>

---

### 엔티티
<details>
   <summary>답안 보기</summary>

- 사람, 장소, 물건, 사건, 개념 등 여러 개의 속성을 지닌 명사를 의미한다.
  - 자동차라는 엔티티는 차 번호, 바퀴 수, 색깔, 차종 등 다양한 속성을 가진다.

</details>

---

### 속성
<details>
   <summary>답안 보기</summary>

- 릴레이션에서 관리하는 구체적이며 고유한 이름을 갖는 정보이다.
  - 필드나 열이라고도 부른다.
- 가령 자동차라는 엔티티는 차 번호, 바퀴 수, 색깔, 차종 등 다양한 속성을 가진다. 이때 서비스에서 필요로 하는 엔티티의 속성을 말한다. 
- 한 릴레이션 안에 있는 애트리뷰트 수를 차수(degree)라고 한다.

</details>

---

### 도메인
<details>
   <summary>답안 보기</summary>

- 릴레이션에 포함된 각각의 속성들이 가질 수 있는 값의 집합을 말한다.
  - 성별이라는 속성의 경우 남자와 여자라는 도메인을 가진다.

</details>

---

### 레코드
<details>
   <summary>답안 보기</summary>

- 테이블에 쌓이는 행단위의 데이터를 레코드라고 한다.
  - 튜플이라고도 한다.
- 릴레이션 튜플의 개수를 카디날리티라고 한다.

</details>

---

### 키
<details>
   <summary>답안 보기</summary>

![image](https://user-images.githubusercontent.com/87891581/189832478-685f412c-c269-43bc-94aa-abc25beee439.png)
- 특정 튜플을 식별할 때 사용하는 속성 혹은 속성의 집합이다.
- 종류로는 슈퍼키, 후보키, 기본키, 대체키가 있다.
- 유일성 : 키의 값들이 서로 중복되지 않음.
- 최소성 : 키가 식별할 수 있는 최소한의 속성들로 구성됨.

</details>

---

### 슈퍼키
<details>
   <summary>답안 보기</summary>

- 튜플을 유일하게 식별하는 속성 혹은 속성의 집합이다.
  - 유일성을 만족하는 키다.
</details>

---

### 후보키
<details>
   <summary>답안 보기</summary>

- 튜플을 유일하게 식별할 수 있는 속성의 최소 집합이다.
- 유일성과 최소성을 만족하는 키다.

</details>

---

### 기본키
<details>
   <summary>답안 보기</summary>

- 여러 후보키 중에서 하나를 선택하여 대표로 선정된 키를 말한다.
- 변경의 여지가 있는 자연키보다는, 인위적으로 기본키를 만들어 사용하는 것을 권장한다.
  - 자연키 : 주민번호와 같이 테이블을 생성하면서 자연스레 존재하는 속성인 기본키를 말한다. 

</details>

---

### 대체키
<details>
   <summary>답안 보기</summary>

- 기본키로 선정되지 않은 후보키를 말한다.

</details>

---

### 외래키
<details>
   <summary>답안 보기</summary>

- 다른 릴레이션의 기본키를 참조하는 속성을 말한다. 
- 기본키와 달리 NULL값과 중복값을 허용한다.

</details>

---

### ERD
<details>
   <summary>답안 보기</summary>

- Entity Relationship Diagram
- 데이터베이스를 구축할 때 가장 기초적인 뼈대 역할을 하며, 릴레이션 간의 관계를 정의한 것을 말한다.

</details>

---

### 이상현상
<details>
   <summary>답안 보기</summary>

- 잘못 설계된 테이블로 삽입, 삭제, 수정 같은 데이터 조작을 할 때 의도와 다르게 동작하는 현상을 말한다.
- 삽입 이상 : 튜플 삽입 시 특정 속성에 해당하는 값이 없어 NULL 값을 입력해야 하는 경우
- 삭제 이상 : 튜플 삭제 시 같이 저장된 다른 정보까지 삭제되는 경우
- 수정 이상 : 튜플 수정 시 중복으로 저장된 데이터 일부만 수정되어 데이터가 일치하지 않는 경우

</details>

---

### 함수 종속성
<details>
   <summary>답안 보기</summary>

- 릴레이션 속성간에 함수적으로 종속하는 성질을 함수 종속성이라고 한다.
  - 어떤 릴레이션에 속하는 속성의 집합 A와 B가 있을 때, A의 값을 알면 B의 값이 유일하게 정해지는 의존 관계를 `Y는 X에 함수 종속`이라고 표현한다.
    - `A -> B`로 표기한다.
    - 이때 A를 결정자라고 하고, B를 종속자라고 한다.

</details>

---

### 정규화
<details>
   <summary>답안 보기</summary>

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

</details>

---

### 반정규화(비정규화)
<details>
   <summary>답안 보기</summary>

- 조인으로 인한 성능 저하와 같은 이유로, 조회 성능 향상을 위해 정규화를 되돌리는 것을 말한다.

</details>

---

### 템플릿
<details>
   <summary>답안 보기</summary>



</details>

---
