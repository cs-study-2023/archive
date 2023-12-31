# Reflection

## 개념정리

### 🪞Reflection이란?

- Java는 JavaScript, Python 등과 같은 언어들과 다르게 정적 언어이다. 그렇기 때문에 데이터 타입을 포함한 클래스 타입, 필드, 메서드들이 컴파일 타임에 이미 결정이 되어있어야 한다.
  - Reflection 기능 지원하지 않는 언어들 : C, C++, Pascal
- 구체적인 클래스 타입을 알지 못해도 그 클래스의 메소드, 타입, 변수들에 접근할 수 있도록 해주는 자바 API를 의미
- Reflection이라는 단어의 사전적 의미는 **반사**이다. 자바 세상에서 Class가 JVM 메모리에 반사되어 있는 것을 의미한다.
  - ![Alt text](img/reflection_classloader.png)
  - JVM은 클래스 정보를 클래스 로더를 통해 읽어와서 해당 정보를 JVM 메모리에 저장한다.
  - 힙 영역에 로드된 Class 타입의 객체를 통해, 원하는 클래스의 인스턴스를 생성할 수 있도록 지원

### Class 클래스

- `Class 클래스`는 `java.lang` 패키지에서 제공되는 실행중인 자바 어플리케여션의 클래스와 인터페이스의 정보를 가진 클래스
- public 생성자가 존재하지 않는다.
- Class 객체는 JVM에 의해 자동으로 생성된다.

### Class의 기능들

- 클래스에 붙은 어노테이션 조회
- 클래스 생성자 조회
- 클래스 필드 조회
- 클래스 메서드 조회
- 부모 클래스, 인터페이스 조회

### Class 객체 가져오기

- **{클래스타입}.class**

```java
Class<?> class = Cat.class;
```

- **{인스턴스}.getClass()**

```java
Cat cat = new Cat("삐삐");
Class<?> class = cat.getClass();
```

- **Class.forName("${전체 도메인 이름}")**

```java
Class<?> class = Class.forName("org.example.Cat");
```

### getMethods vs getDeclaredMethods

- getMethods : 상위 클래스와 상위 인터페이스에서 **상속한 메서드를 포함**하여 **public**인 메서드들을 모두 가져온다
- getDeclaredMethods : 접근 제어자와 관계 없이 상속한 메서드를 제외하고 **직접 클래스에서 선언한 메서드들**을 모두 가져온다

### Reflection을 사용하는 경우

- 클래스를 활용하는 코드를 작성하는 시점에서 어떤 클래스가 사용될지 모르는 경우
  - 프레임워크나 라이브러리에서 주로 사용됨
  - Spring Framework의 어노테이션 기능이 대표적이라 한다.
    - #### 어노테이션은 작동 순서
      1. Reflection을 통해 클래스나 메서드, 파라미터 정보를 가져온다.
      2. Reflection의 getAnnotation(s), getDeclaredAnnotation(s)등의 메서드를 통해 원하는 어노테이션이 붙어있는지 확인한다.
      3. 어노테이션이 붙어 있다면 원하는 로직을 수행한다.
- 예시
  1. JPA
  2. Jackson : JSON 처리
  3. Mockito : 테스트 코드
  4. Intellij 자동완성 기능

### 기본 생성자의 필요성

- JPA Entity, RequestDTO, ResponseDTO는 기본생성자를 필요로 한다
- Reflection으로 객체를 생성가능한데, 또 기본 생성자를 필요로하는 이유는 기본 생성자로 객체를 생성하고, 필드를 통해 값을 넣어주는 것이 가장 간단한 방법이기 때문이다.
  - 생성자가 여러개일 경우 특정 생성자를 고르기 힘들다.
  - 생성자에 로직 있는 경우 원하는 값을 바로 넣어줄 수 없다.
  - 파라미터들의 타입이 같은 경우, 필드와 이름이 다르면 값을 알맞게 넣어주기 힘들다
  - 기본 생성자를 사용할 경우 이 모든 경우의 수를 고려하지 않아도 된다. -> 기본 생성자로 객체를 생성 후 필드 이름에 맞춰 알맞은 값을 넣어주면 끝!!

### Reflection의 장단점

#### 장점

- 런타임 시점에서 클래스의 인스턴스를 생성하고, 접근 제어자와 관계 없이 필드와 메서드에 접근하여 필요한 작업을 수행할 수 있는 유연성을 지님

#### 단점

- 일반 메서드 호출보다 성능이 훨씬 떨어진다
  - Reflection API는 컴파일 시점이 아니라 런타임 시점에서 클래스를 분석하기에 JVM을 최적화 할 수 없기 때문에 성능 저하 발생
- 컴파일 시점에서 타입 체크 기능을 사용할 수 없다.
  - 컴파일 시점에 제공하는 type check 기능 사용 불가 -> ClassNotFoundException 발생 가능
- 코드가 지저분해지고 장황해진다.
- 내부를 노출해서 추상화를 파괴한다.
  - 접근할 수 없는 필드, 메서드에 접근 가능하며 모든 클래스의 정보 확인 가능

### Reflection 사용 이유

- 동적인 객체 생성: Reflection을 사용하면 런타임 시에 클래스의 인스턴스를 동적으로 생성할 수 있습니다. 클래스 이름을 동적으로 전달하여 객체를 생성할 수 있으며, 이는 유연한 객체 생성 패턴을 구현하는 데 도움이 됩니다.

- 클래스 정보 조사: Reflection은 클래스의 메서드, 필드, 상위 클래스, 인터페이스 등의 정보를 동적으로 조사할 수 있습니다. 이를 통해 프로그램이 실행 중에 클래스의 구조를 분석하고 다양한 작업을 수행할 수 있습니다. 예를 들어, 특정 어노테이션을 가진 메서드를 찾거나, 클래스의 필드 값을 변경할 수 있습니다.

- 동적 메서드 호출: Reflection을 사용하면 메서드의 이름과 매개변수를 동적으로 지정하여 메서드를 호출할 수 있습니다. 이는 일반적으로 알려지지 않은 클래스나 인터페이스와 상호작용해야 할 때 유용합니다. 예를 들어, 외부 라이브러리나 플러그인 시스템과의 통합에 활용할 수 있습니다.

- 애노테이션 처리: Reflection을 사용하면 애노테이션 정보를 읽고 처리할 수 있습니다. 런타임 시에 애노테이션을 분석하여 특정 작업을 수행하거나, 애노테이션을 기반으로 동적으로 코드를 생성할 수 있습니다. 이는 프레임워크나 라이브러리에서 커스텀 애노테이션을 활용하여 기능을 확장하거나, 실행 중에 설정 정보를 처리하는 데 사용됩니다.

- 리소스 접근: Reflection을 사용하면 클래스로더를 통해 리소스에 접근할 수 있습니다. 클래스 경로에 있는 파일이나 설정 파일 등을 동적으로 로드하여 사용할 수 있습니다.

### 주의 사항

- Reflection은 강력한 기능이지만, 실행 시간에 타입 검사를 회피하고 퍼포먼스 저하를 일으킬 수 있다.
- 코드의 복잡성을 증가시킬 수 있으므로 신중하게 사용해야 한다.
- 주로 프레임워크, 라이브러리, 개발자 도구 등의 개발에 활용되며, 일반적인 애플리케이션 개발에서는 Reflection을 적게 사용하는 것이 좋다.

---

## 예상 질문

- 리플렉션(Reflection)이란 무엇인지 설명해주세요
- 리플렉션은 어떤 경우에 사용되는지 설명해주세요.

---

### 참고자료

[https://github.com/devFancy/2023-CS-Study](https://github.com/devFancy/2023-CS-Study/blob/main/java/java_reflection.md)
