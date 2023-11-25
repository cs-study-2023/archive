### Transaction ?

**데이터베이스의 데이터를 조작하는 작업의 단위(unit of work)**이다. 가장 많이 드는 예시는 계좌이체이다.

다음과 같은 예시를 들어보면 쉽게 이해할 수 있다.

1. A 계좌 잔액 확인
2. A 계좌의 금액에서 이체할 금액을 빼고 다시 저장한다.
3. B 계좌의 잔액을 확인한다.
4. B 계좌의 금액에 이체할 금액을 더하고 다시 저장한다.

이러한 과정은 모두 합친 계좌 이체라는 하나의 작업 단위를 구성한다. 여기서 하나의 작업 단위는 commit 되거나 rollback이 된다. \*\*\*\*

- **Commit**
  한 가지의 논리적인 단위에 대한 작업이 성공적으로 끝나 DB가 다시 일관된 상태에 있을 때 앞의 작업 완료를 관리자에게 알려주는 연산이다.
- **Rollback**
  작업 단위 중 하나의 처리가 비정상적으로 종료가 돼 DB 일관성을 깨뜨렸을 때, 이 부분 완료 상태일지라도 원자성의 특징을 지키기 위해 모든 연산을 취소(undo)하는 연산이다.

### ACID ?

- Atomicity (원자성)
  하나의 작업 단위(트랜잭션)의 연산이 DB에 모두 반영되던지 전혀 반영이되지 않던지 둘중에 하나만 수행해야한다.
- Consistency (일관성)
  트랜잭션이 성공적으로 완료된 후에는 언제나 일관성 있는 DB상태로 변환되어야한다.
- Isolation (독립성)
  하나의 트랜잭션이 실행하는 도중에 변경한 데이터는 이 트랜잭션이 완료될 때 까지 다른 트랜잭션이 참조하지 못한다
- Durablility (영속성)
  성공적으로 완료된 결과는 영구적으로 반영되어야 한다.

### State ?

- **활동 (Active)**
  트랜잭션이 실행 중에 있는 상태, 연산들이 정상적으로 실행 중인 상태
- **장애 (Failed)**
  트랜잭션이 실행에 오류가 발생하여 중단된 상태
- **철회 (Aborted)**
  트랜잭션이 비정상적으로 종료되어 Rollback 연산을 수행한 상태
- **부분 완료 (Partially Committed)**
  트랜잭션이 마지막 연산까지 실행했지만, Commit 연산이 실행되기 직전의 상태
- **완료 (Committed)**
  트랜잭션이 성공적으로 종료되어 Commit 연산응 실행한 후의 상태

### ACID는 완벽하게 지켜지지 않는다.

ACID 원칙을 지키려면 동시성이 매우 떨어지게 된다. 그렇기에 db 엔진은 원칙을 위배해서 동시성을 얻을 수 있는 방법을 제공하게 된다. 바로 Transaction의 isolation level 이다. isolation 원칙을 덜 지키는 level을 사용할수록 문제가 발생할 가능성은 커지지만 동시에 더 높은 동시성을 얻을 수 있다.

### Lock

Lock은 트랜잭션 처리의 순차성을 보장하기 위한 방법으로, DBMS에 따라 다양한 방식과 세부적인 방법으로 구현됩니다.

**Lock의 종류:**

- **공유(Shared) Lock:** 데이터를 읽을 때 사용되며, 여러 사용자가 동시에 접근 가능합니다.
- **베타(Exclusive) Lock:** 데이터를 변경할 때 사용되며, 해당 리소스에 대한 접근을 다른 트랜잭션이 할 수 없게 합니다.

**블로킹**

- 블로킹은 Lock 간의 경합으로 인해 특정 트랜잭션이 작업을 진행하지 못하고 멈춰선 상태를 나타냅니다.
- 베타 Lock 간이나 베타 Lock과 공유 Lock 간의 경합에서 블로킹이 발생할 수 있습니다.
- 블로킹을 해소하려면 이전 트랜잭션이 완료(커밋 또는 롤백)되어야 합니다.

**블로킹을 최소화하기 위한 주의사항**

- 트랜잭션의 길이를 너무 길게 하지 않는다.
- 설계 단계에서 동시에 같은 데이터를 갱신하는 트랜잭션이 발생하지 않도록 한다.
- 불필요하게 트랜잭션 격리성 수준을 상향 조정하지 않는다.
- 튜닝을 통해 쿼리의 실행 시간을 적절히 조절한다.

**예상 질문**

1. 트랜잭션은 무엇인가요?
2. ACID란 무엇을 나타내는 것이며, 각각의 원칙은 무엇인가요?
3. 트랜잭션의 상태에는 어떤 것들이 있고, 각각은 어떤 의미를 가지나요?
4. 블로킹이란 무엇이며, 어떻게 블로킹을 해소할 수 있나요?
5. Lock은 어떤 목적으로 사용되며, 그 종류에는 어떤 것들이 있나요?
6. ACID 원칙을 완벽하게 지키려면 어떤 문제가 발생할 수 있고, 이를 해결하기 위한 방법은 무엇인가요?