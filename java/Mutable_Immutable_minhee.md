## Mutable, Immutable

- 자바는 new 연산자로 객체를 생성할 수 있고, 이때 heap 영역에 할당되고 stack 영역에서 참조 타입 변수를 통해 데이터에 접근한다.
- 이때 자바 객체의 타입은 mutable, immutable이 있다.

### Immutable(불변) 객체

- 정의
    - 객체 생성 이후에는 객체의 상태가 바뀌지 않는 객체
- 종류
    - String, Boolean, Integer, Float, Long

```jsx
String name = "minhee";
name = "hongseo";
```

### ✔️ String, StringBuilder, StringBuffer

- **String** (`Immutable` 객체)
    - String은 대표적인 Immutable 객체로 읽을 수만 있고 변경은 할 수 없다. (ReadOnly)
    - 이러한 특징 때문에 mutable 객체인 StringBuilder와 StringBuffer를 자주 사용한다.
    - StringBuilder와 StringBuffer의 차이점은 **동기화 지원 유무**이다.
- **StringBuilder** (`Mutable` 객체)
    - StringBuilder는 단일 스레드 환경에서만 사용하도록 설계되어 있다.
- **StringBuffer** (`Mutable` 객체)
    - StringBuffer는 각 메사드 별로 synchronized keyword가 존재하여 멀티 스레드 상태에서 동기화를 지원한다.

### 불변객체를 사용하는 이유

- 단순하다
    - 불변 객체의 상태는 생성된 시점으로부터 파괴되는 시점까지 그대로 유지된다.
- 값의 변경을 방지한다.
    - 불변 객체에 생성 시점에 값을 설정한 후, 변경할 수 없기 때문에 예기치 않은 값 변경을 방지할 수 있다.
- (일반적으로) 스레드 안정성을 어느정도 보장할 수 있다.
    - multi-thread 환경에서 동기화 문제가 발생하는 이유는 공유 자원에 동시 쓰기 연산 때문!
    - 불변객체라면 항상 동일한 값을 반환하고(변경x), 동기화 처리 없이 객체 공유가 가능하다.

### cf. 불변 객체를 구현하는 방법

1. 생성자를 제외하고 객체의 상태를 변경하는 메서드(setter)를 사용하지 않는다.
2. 클래스를 확장할 수 없도록 한다. 
    - (final 키워드 사용하여 상속을 막을 수 있다.)
3. 모든 필드는 private final로 선언하고 생성시 값을 초기화 한다. 
4. 자신 외에는 내부의 가변 컴포넌트에 접근할 수 없도록 한다.


## 출처
https://github.com/devSquad-study/2023-CS-Study/blob/main/java/java_mutable_immutable.md

## 질문
> Mutable 객체와 Immutable 객체의 차이점에 대해 설명해주세요.

> 불변 객체를 사용하는 이유가 무엇이라고 생각하세요?