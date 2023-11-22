# View(뷰)

## 개념정리

### 정의

- View는 사용자에 따라 **정보를 제한적으로 제공**하기 위해 하나 이상의 기본 테이블로부터 유도된 가상 테이블이다.
- **보안**을 위해 사용한다.
- 예를 들어 Professor table을 공개하되 salary(연봉) 정보는 제외한 컬럼들만 공개하고 싶다는 요구사항이 있을 때 View를 사용한다.

```mysql
CREATE VIEW faculty AS
SELECT pID, name, deptName FROM Professor;
```

- View는 Virtual Relation이라고 불리기도 한다.

### 특징

- 기본 테이블로부터 유도된 테이블이므로 기본테이블과 같은 구조를 가지며 조작 또한 기본 테이블과 거의 같다.
- View는 실제 Table을 다른 창구로 바라보는 것이므로 항상 최신의 데이터를 가지고 있다.
- 물리적으로 존재하지 않고, 논리적으로만 존재한다.
- 데이터의 논리적 독립성을 제공해 데이터 관리가 용이하다.
  - 데이터의 물리적인 구조나 저장 방식과 독립적으로 데이터를 접근할 수 있다.
  - 복잡한 데이터 구조를 몰라도 데이터에 접근 가능하다.
  - 예를 들어, 데이터의 복잡한 쿼리를 숨기는 인터페이스 역할을 할 수 있다.
- View에 나타나지 않는 데이터를 보호할 수 있다.
- 기본키를 포함한 속성으로 View를 구성해야 삽입, 삭제, 갱신 연산이 가능하다.
- View를 이용해 또 다른 View를 정의할 수도 있다.
  - 다른 View의 기초가 되는 View를 삭제 시 연쇄 삭제가 일어날 수도 있다.

### View Expansion

- View에 대해서 SELECT 쿼리(조회 업무)가 이루어질 때 View에 대한 정의(Definition query)로 치환되어 처리되는 것을 말한다.
- 즉, 사용자가 View를 조회하는 쿼리를 실행하면 시스템은 해당 View의 정의에따라 필요한 테이블이나 조건들을 실제 쿼리로 변환해 데이터를 가져오게 한다.

```mysql
SELECT * FROM faculty;
```

(치환)

```mysql
SELECT * FROM (SELECT pID, name, deptName FROM Professor);
```

### View Modification

- View는 특정 제약 하에서는 기본 테이블에 수정을 허용한다.
- View에 없는 컬럼이 null을 허용해야한다.

```mysql
INSERT INTO faculty VALUES (‘30765’, ‘Yang’, ‘CS’);
```

(치환)

```mysql
INSERT INTO Professor VALUES (‘30765’, ‘Yang’, ‘CS’, null);
```

- View가 단일 테이블에 연관되어 있어야한다.
  - 이 경우 어디 deptName으로 할지 결정할 수 없어 수정이 불가능하다.

```mysql
CREATE VIEW professorInfo as
SELECT pID, name, building FROM professor, department
WHERE professor.deptName = department.deptName
```

```mysql
INSERT INTO professorInfo VALUES (‘666’, ‘White’, ‘Taylor’);
```

- 집계함수 혹은 distinct, group by가 있으면 안된다.
  - 이 경우 기본 테이블인 professor 테이블을 어떻게 변경할지 결정 불가능하다.

```mysql
CREATE VIEW departmentTotalSalary(deptName, totalSalary) AS
SELECT deptName, SUM(salary) FROM professor
GROUP BY deptName;
```

```mysql
INSERT INTO departmentTotalSalary VALUES (‘CS’, 100,000);
```

- WITH CHECK OPTION
  - CSProfessors 는 ‘CS’ 학과 교수에 관련된 View
  - 근데 수학과 교수를 추가하는 논리적인 오류를 범하고 있다.
  - 이를 막기 위한 옵션으로 CREATE View 구문 맨 끝에 WITH CHECK OPTION 을 붙여주면 이를 막는다.

```mysql
CREATE VIEW CSProfessors AS
SELECT * FROM professor WHERE deptName = ‘CS’ WITH CHECK OPTION;
```

```mysql
INSERT INTO CSProfessors VALUES (‘255’, ‘Brown’, ‘Math’, 1000); # 에러 발생
```

### 한계

- View에 대해서는 index를 만들지 않는다.
  - View 자체에는 데이터가 물리적으로 저장되지 않기 때문에, View에 직접 인덱스를 생성하는 것은 불가능하다.
  - View를 구성하는 기존의 테이블에 대해 인덱스가 생성되어 있다면 View를 쿼리하는 경우에 이를 활용할 수 있다. 하지만 View 자체에 대한 인덱스 생성은 불가능하다.
- View에 대해서는 key와 constraint를 생성할 수 없다.
  - View에 대해서는 별도로 기본키나 외래키 등과 같은 키나 제약 조건을 생성할 수 없다.
  - View는 기존의 테이블로부터 데이터를 가공, 필터링, 조인하는 등의 작업을 수행하는 논리적인 구조이기 때문에, View 자체에 키나 제약 조건을 부여하는 것은 허용되지 않는다.
- View는 가상의 개념이며, 기존의 데이터베이스 객체를 기반으로 데이터를 가공하고 제한된 형태로 표현하는데 그 목적이 있기 때문에 이러한 한계가 존재한다.

## 예상질문

- View를 설명해보세요.
  - 사용 정의와 사용 특징 정도로만 대답할 수 있으면 된다.

---

### 참고자료

[[DB]Mysql View](https://bubble-dev.tistory.com/entry/DB-Mysql-View)<br>
[[데이터베이스] 뷰(View)](https://dheldh77.tistory.com/entry/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4-%EB%B7%B0View)<br>
