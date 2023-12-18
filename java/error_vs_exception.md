# Error VS Exception

## 오류(error)와 예외(exception)

오류(Error)는 시스템에 비정상적인 상황이 생겼을 때 발생한다. 이는 시스템 레벨에서 발생하기 때문에 심각한 수준의 오류이다. 따라서 개발자가 미리 예측하여 처리할 수 없으므로, 애플리케이션에서 오류에 대한 처리를 신경쓰지 않아도 된다.  
예외(Exception)는 개발자가 구현한 로직에서 발생한다. 즉, 예외는 발생할 상황을 미리 예측하여 처리할 수 있다. 즉, 예외는 개발자가 처리할 수 있기 때문에 예외를 구분하고 그에 따른 처리 방법을 명확히 알고 적용하는 것이 중요하다.

## 예외클래스

![예외클래스 구조도](img/exeption_class.png)

위 그림은 예외클래스의 구조이다. 모든 예외클래스는 Throwable 클래스를 상속받고 있으며, Throwable은 최상위 클래스 Object의 자식 클래스이다.

Trowable을 상속받는 클래스는 Error와 Exception이 있다. Error는 시스템 레벨의 심각한 수준의 에러이기 때문에 시스템에 변화를 주어 문제를 처리해야 하는 경우가 일반적이다. 반면에 Exception은 개발자가 로직을 추가하여 처리할 수 있다.

Exception은 수많은 자식클래스를 가지고 있다. 그 중 RuntimeException을 주목해야 한다. RuntimeException은 CheckedException과 UncheckedException을 구분하는 기준이다. Exception의 자식 클래스 중 RuntimeException을 제외한 모든 클래스는 CheckedException이며, RuntimeException과 그의 자식 클래스들을 Unchecked Exception이라 부른다.

## Checked Exception과 Unchecked(Runtime) Exception

![예외클래스 구조도](img/exception_table.png)

1. Checked Exception과 Unchecked Exception의 가장 명확한 구분 기준은 ‘꼭 처리를 해야 하느냐’이다.  
   Checked Exception이 발생할 가능성이 있는 메소드라면 반드시 로직을 try/catch로 감싸거나 throw로 던져서 처리해야 한다. 반면에 Unchecked Exception은 명시적인 예외처리를 하지 않아도 된다. 이 예외는 피할 수 있지만 개발자가 부주의해서 발생하는 경우가 대부분이고, 미리 예측하지 못했던 상황에서 발생하는 예외가 아니기 때문에 굳이 로직으로 처리를 할 필요가 없도록 만들어져 있다.

2. 예외를 확인할 수 있는 시점에서도 구분할 수 있다.  
   일반적으로 컴파일 단계에서 명확하게 Exception 체크가 가능한 것을 Checked Exception이라 하며, 실행과정 중 어떠한 특정 논리에 의해 발견되는 Exception을 Unchecked Exception이라 한다. 따라서 컴파일 단계에서 확인할 수 없는 예외라 하여 Unchecked Exception이며, 실행과정 중 발견된다 하여서 Runtime Exception이라 하는 것이다. (+ Unchecked Exception은 컴파일 시점에 예외를 catch하는지 확인하지 않는다. 따라서 컴파일 시점에 예외가 발생하는지 여부를 확인할 수 없다.)

3. 마지막으로 예외발생시 트랜잭션의 roll-back 여부가 있다.  
   기본적으로 Checked Exception은 예외가 발생하면 트랜잭션을 roll-back하지 않고 예외를 던져준다. 하지만 Unchecked Exception은 예외 발생 시 트랜잭션을 roll-back한다는 점에서 차이가 있다. 트랜잭션의 전파방식 즉, 어떻게 묶어놓느냐에 따라서 Checked Exception이냐 Unchecked Exception이냐의 영향도가 크다. roll-back이 되는 범위가 달라지기 때문에 개발자가 이를 인지하지 못하면, 실행결과가 맞지 않거나 예상치 못한 예외가 발생할 수 있다. 그러므로 이를 인지하고 트랜잭션을 적용시킬 때 전파방식(propagation behavior)과 롤백규칙 등을 적절히 사용하면 더욱 효율적인 애플리케이션을 구현할 수 있을 것이다.

## 예외 처리 방법

![예외클래스 구조도](img/exception1.jpg)  
위 그림은 예외를 처리하는 일반적인 방법 3가지이다.

1. 다른 작업 흐름으로 유도하는 예외 복구
2. 처리를 하지 않고 호출한 쪽으로 던져버리는 예외처리 회피
3. 호출한 쪽으로 던질 때 명확한 의미를 전달하기 위해 다른 예외로 전환하여 던지는 예외 전환

### 1) 예외 복구

```java
int maxretry = MAX_RETRY;
while(maxretry -- > 0) {
    try {
        // 예외가 발생할 가능성이 있는 시도
        return; // 작업성공시 리턴
    }
    catch (SomeException e) {
        // 로그 출력. 정해진 시간만큼 대기
    }
    finally {
        // 리소스 반납 및 정리 작업
    }
}
throw new RetryFailedException(); // 최대 재시도 횟수를 넘기면 직접 예외 발생
```

예외복구의 핵심은 예외가 발생하여도 애플리케이션은 정상적인 흐름으로 진행된다는 것이다.  
위 코드는 재시도를 통해 예외를 복구하는 코드이다. 이 예제는 네트워크가 환경이 좋지 않아서 서버에 접속이 안되는 상황의 시스템에 적용하면 효율적이다. 예외가 발생하면 그 예외를 잡아서 일정 시간만큼 대기하고 다시 재시도를 반복한다. 그리고 최대 재시도 횟수를 넘기면 예외를 발생시킨다. 재시도를 통해 정상적인 흐름을 타게 한다거나, 예외가 발생하면 이를 미리 예측하여 다른 흐름으로 유도시키도록 구현하면 비록 예외가 발생하였어도 정상적으로 작업을 종료할 수 있을 것이다.

### 2) 예외처리 회피

```java
public void add() throws SQLException {
... // 구현 로직
}
```

위 코드는 간단해 보이지만 아주 신중해야하는 로직이다. 예외가 발생하면 throws를 통해 호출한쪽으로 예외를 던지고 그 처리를 회피하는 것이다. 하지만 무책임하게 던지는 것은 위험하다. 호출한 쪽에서 다시 예외를 받아 처리하도록 하거나, 해당 메소드에서 이 예외를 던지는 것이 최선의 방법이라는 확신이 있을 때만 사용해야 한다.

### 3) 예외 전환

```java
catch(SQLException e) {
   ...
   throw DuplicateUserIdException();
}
```

예외 전환은 위 코드에서 처럼 예외를 잡아서 다른 예외를 던지는 것이다. 호출한 쪽에서 예외를 받아서 처리할 때 좀 더 명확하게 인지할 수 있도록 돕기 위한 방법이다. 어떤 예외인지 분명해야 처리가 수월해지기 때문이다. 예를 들어 Checked Exception 중 복구가 불가능한 예외가 잡혔다면 이를 Unchecked Exception으로 전환하여서 다른 계층에서 일일이 예외를 선언할 필요가 없도록 할 수도 있다.

초급 개발자가 가장 잊지 말아야 할 것은 예외를 잡고 아무런 처리도 하지 않는 것은 정말 위험한 행위라는 것이다. try/catch문으로 예외를 잡아놓고 catch를 비워두면 물론 컴파일 오류는 나지 않겠지만, 예외가 발생했을 때 그 원인을 파악하기가 어려워 개발은 물론 유지보수에 아주 치명적인 민폐를 끼치는 일이라고 생각한다. 따라서 어떤 처리를 해야 하는지 모르더라도 무작정 catch하고 무시하거나, throw해버리는 행위를 할 때는 더욱 신중해야 할 것이다.

## 예상 질문

- Checked Exception과 Unchecked Exception에 대해 말해주세요
- Error과 Exception의 차이를 설명해주세요

## 참고 링크

https://www.nextree.co.kr/p3239/  
https://github.com/devSquad-study/2023-CS-Study/blob/main/java/java_error_vs_exception.md
