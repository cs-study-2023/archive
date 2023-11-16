# Join(조인)

## 개념정리

### 정의

- 하나의 테이블이 아닌 두 개 이상의 테이블을 묶어서 하나의 결과물을 만드는 것이다.
- MySQL에서는 JOIN이라는 쿼리로 MongoDB에서는 lookup이라는 쿼리로 이를 처리한다.

> 하지만 NoSQL인 MongoDB는 조인 연산에 대해 관계형 데이터베이스보다 성능이 떨어지는 결과가 여러 벤치마크 테스트에서 알려져 있으므로 조인 작업이 필요한 경우는 관계형 데이터베이스를 사용해야한다.

### 종류

#### 내부 조인(inner join)

- 왼쪽 테이블과 오른쪽 테이블의 두 행이 **모두 일치**하는 행이 있는 부분만 표기
  - 즉, 두 테이블 간에 교집합을 나타낸다.

```sql
SELCET * FROM TableA A
INNER JOIN TableB B ON A.key = B.key
(WHERE ~~~)
```

![](https://velog.velcdn.com/images/newdana01/post/183207d2-b0eb-4754-bb45-26905f5d7ffa/image.png)
![](https://velog.velcdn.com/images/newdana01/post/f698a65c-bc7e-44f0-85f2-268215e9876d/image.png)
![](https://velog.velcdn.com/images/newdana01/post/2b57131d-003f-4287-9f46-11a93a460478/image.png)

#### 왼쪽 조인(left outer join)

- 왼쪽 테이블의 모든 행이 결과 테이블에 표기
- 왼쪽 조인은 테이블 B의 일치하는 부분의 레코드와 함께 테이블 A를 기준으로 완전한 레코드 집합을 생성
- 만약 테이블 B에 일치하는 항목이 없으면 해당 값은 null 값이 된다.

```sql
SELECT * FROM TableA A
LEFT JOIN TableB ON A.key = B.key
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F994ECC3F5C0D1ED21C)
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F99C530425C0D1ED30A)

#### 오른쪽 조인(right outer join)

- 오른쪽 테이블의 모든 행이 결과 테이블에 표기
- 오른쪽 조인은 테이블 A에서 일치하는 부분의 레코드와 함께 테이블 B를 기준으로 완전한 레코드 집합을 생성
- 만약 A에 일치하는 항목이 없으면 해당 값은 null값이 된다.

```sql
SELECT * FROM TableA A
RIGTH JOIN TableB ON A.key = B.key
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F99943F4D5C0D1ED536)
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F99D5FD485C0D1ED51A)

#### 완전 외부 조인(full outer join)

- 두 개의 테이블을 기반으로 조인
- **조건에 만족하지 않는 행까지 모두** 표기
- 합집합 조인(완전 외부 조인)은 양쪽 테이블에서 일치하는 레코드와 함께 테이블 A와 테이블 B의 모든 레코드 집합을 생성.
- 이때 일치하는 항목이 없으면 누락된 쪽에 null값이 포함되어 출력

```sql
SELECT * FROM TableA A
FULL OUTER JOIN Table B ON A.key = B.key
```

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F99270C3E5C0D1ED70D)
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F9932304C5C0D1ED735)

### 조인의 원리

- 앞서 설명한 조인은 조인의 원리를 기반으로 작업이 이루어진다.
- 조인의 원리인 중첩 루프 조인, 정렬 병합 조인, 해시 조인이 존재

#### 중첩 루프 조인(NLJ, Nested Loop Join)

- 중첩 for문과 같은 원리로 조건에 맞는 조인을 하는 방법
- 랜덤 접근에 대한 비용이 많이 증가하므로 대용량의 테이블에서는 사용하지 X
- ex) "t1, t2 테이블을 조인한다"라고 하면 첫번 째 테이블에서 행을 한번에 하나씩 읽고 그 다음 테이블에서도 행을 하나씩 읽어 조건에 맞는 레코드를 찾아 결괏값을 반환

```
<의사 코드>
for each row in t1 matching reference key {
	for each row in t2 matching reference key {
    	if row satisfies jion conditions, send to client
        }
    }
```

> 💡 참고
> 중첩 루프 조인에서 발전한 조인할 테이블을 작은 블록으로 나눠서 블록 하나씩 조인하는 블록 중첩 루프 조인(Block Nested Loop)라는 방식도 존재

#### 정렬 병합 조인

- 각각의 테이블을 조인할 필드 기준으로 정렬하고 정렬이 끝난 이후로 조인 작업을 수행하는 조인
- 조인할 때 쓸 적절한 인덱스가 없고 대용량의 테이블들을 조인하고 조인 조건으로 <,> 등 범위 비교 연산자가 있을 때 사용

#### 해시 조인

- 해시 테이블을 기반으로 조인하는 방법
- 두개의 테이블을 조인한다고 했을 때 하나의 테이블의 메모리에 온전히 들어간다면 보통 중첩 루프 조인보다 더 효율적.(메모리에 올릴 수 없을 정도로 크다면 디스크를 사용하는 비용이 발생)
- 동등(=)조인에서만 사용 가능

> MySQL의 경우 MySQL8.0.18 릴리스와 함께 이 기능을 사용할 수 있게 되었으며 이를 기반으로 하는 조인의 과정을 살펴보자.

- MySQL의 해시 조인 단계
  - 빌드 단계, 프로브 단계로 나뉜다.
  - 빌드 단계
    - 입력 테이블 중 하나를 기반으로 메모리 내 해시 테이블을 빌드하는 단계
    - persons와 countries라는 테이블을 조인한다고 했을 때 둘 중에 바이트가 더 작은 테이블을 기반으로 해서 테이블을 빌드
    - 또한 조인에 사용되는 필드가 해시 테이블의 키로 사용.(countries.country_id가 키로 사용되는 것 확인 가능)
    - ![](https://velog.velcdn.com/images/pjh1011409/post/b49060bd-c1b3-4b8f-8210-05e63fc92f4e/image.png)
  - 프로브 단계
    - 프로브 단계 동안 레코드 읽기를 시작하며, 각 레코드에서 'Person.country_id'에 일치하는 레코드를 찾아서 결괏값으로 반환
    - 이를 통해 각 테이블은 한 번씩만 읽게 되어 중첩해서 두개의 테이블을 읽는 중첩 루프조인보다 보통은 성능이 더 좋다. 참고로 사용 가능한 메모리양은 시스템 변수 join_buffer_size에 의해 제어되며, 런타임 시에 조정 가능
    - ![](https://velog.velcdn.com/images/pjh1011409/post/82f2369a-c583-4f5d-bef7-52696411605e/image.png)

---

## 예상 질문

- inner join과 outer join의 차이를 설명해주세요.
- JOIN에서 ON과 WHERE의 차이를 설명해주세요.
- 중첩 루프 조인은 무엇인가?

---

### 참고자료

https://velog.io/@pjh1011409/CS-%EC%A0%84%EA%B3%B5%EC%A7%80%EC%8B%9Djoin

출처: https://dev-coco.tistory.com/158 [슬기로운 개발생활:티스토리]

https://advenoh.tistory.com/23
