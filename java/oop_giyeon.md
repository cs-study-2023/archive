# 객체지향 프로그래밍(Object Oriented Programming, OOP)

## 객체 지향 프로그래밍이란

우리가 실생활에서 쓰는 모든 것을 객체라 하며, 객체 지향 프로그래밍은 프로그램 구현에 필요한 객체를 파악하고 상태와 행위를 가진 객체를 만들고 각각의 객체들의 역할이 무엇인지를 정의하여 객체들 간의 상호작용을 통해 프로그램을 만드는 것을 말햔다.

즉, 기능이 아닌 객체가 중심이며 "누가 어떤 일을 할 것인가?"가 핵심

## 객체지향 장단점

### 장점

- 코드 재사용이 용이  
  남이 만든 클래스를 가져와서 이용할 수 있고 상속을 통해 확장해서 사용할 수 있다.

- 유지보수가 쉬움  
  절차 지향 프로그래밍에서는 코드를 수정해야할 때 일일이 찾아 수정해야하는 반면 객체 지향 프로그래밍에서는 수정해야 할 부분이 클래스 내부에 멤버 변수혹은 메서드로 존재하기 때문에 해당 부분만 수정하면 된다.

- 대형 프로젝트에 적합  
  클래스 단위로 모듈화시켜서 개발할 수 있으므로 대형 프로젝트처럼 여러 명, 여러 회사에서 프로젝트를 개발할 때 업무 분담하기 쉽다.

### 단점

- 처리 속도가 상대적으로 느림
- 객체가 많으면 용량이 커질 수 있음
- 설계시 많은 시간과 노력이 필요

## 객체지향 특징

객체지향의 주요한 키워드로는 아래 다섯가지가 있다.

1. 클래스 + 인스턴스(객체)
2. 추상화
3. 캡슐화
4. 상속
5. 다형성

### 1. 클래스와 인스턴스(객체)

클래스: 어떤 문제를 해결하기 위한 데이터를 만들기 위해 추상화를 거쳐 집단에 속하는 속성(attribute)과 행위(behavior)를 변수와 메서드로 정의한 것으로 객체를 만들기 위한 메타정보라고 볼 수 있다.

인스턴스(객체) : 클래스에서 정의한 것을 토대로 실제 메모리에 할당된 것으로 실제 프로그램에서 사용되는 데이터

### 2. 추상화(자료의 추상화)

객체 지향 프로그래밍에서는 '추상화' 라는 단어를 여러 군데 붙일 수 있다.  
여기서 말하는 추상화는 추상 클래스나 추상 클래스가 갖는 추상 메서드를 의미하기보다는 클래스를 설계하는 것 자체를 의미한다.
즉, "공통의" 속성이나 기능을 묶어 이름을 붙이는 것이다.

### 3. 캡슐화

캡슐화의 목적 2가지:

1. 코드를 재수정 없이 재활용하는 것.
2. 접근 제어자를 통한 정보 은닉

절차 지향 프로그래밍에서도 라이브러리를 통해서 변수와 함수를 재활용할 수는 있었지만, 코드의 수정이 일어났을 때 영향 범위를 예상하기 어려운 문제가 있었다.

그러나 객체 지향 프로그래밍에서는 캡슐화를 통해 객체가 외부에 노출하지 않아야할 정보 또는 기능을 접근제어자를 통해 적절히 제어 권한이 있는 객체에서만 접근하도록 할 수 있기에 코드의 수정이 일어났을 때 책임이 있는 객체만 수정하면 되기에 영향 범위를 예측하는데 수월해졌다.

뿐만 아니라 관련된 기능과 특성을 한 곳에 모으고 분류하기 때문에 객체 재활용이 원활해졌다.  
객체 지향 프로그래밍에서 기능과 특성의 모음을 "클래스"라는 "캡슐"에 분류해서 넣는것이 캡슐화다.
객체가 맡은 역할을 수행하기 위한 하나의 목적을 한데 묶는다.

### 4. 상속

절자 지향 프로그래밍에서도 "라이브러리"를 통해서 남이 짜놓은 소스 코드를 가져와 사용할 수 있었다. 하지만 내 의도에 맞게 수정하게 되면 다른 라이브러리가 되어 버전에 따라 동작하지 않을 수 있고 불필요한 코드의 수정작업을 해야한다.  
이런 문제를 해결하기 위해 [상속]이라는 것을 도입하였다.

상속은 부모클래스의 속성과 기능을 그대로 이어받아 사용할 수 있게하고 기능의 일부분을 변경해야 할 경우 상속받은 자식클래스에서 해당 기능만 다시 수정(정의)하여 사용할 수 있게 하는 것이다.

### 5. 다형성

하나의 변수명, 함수명 등이 상황에 따라 다른 의미로 해석될 수 있는 것이다.  
즉 오버라이딩(Overriding), 오버로딩(Overloading)이 가능하다는 얘기다.

오버라이딩 : 부모클래스의 메서드와 같은 이름, 매개변수를 재정의 하는것.  
오버로딩 : 같은 이름의 함수를 여러개 정의하고, 매개변수의 타입과 개수를 다르게 하여 매개변수에 따라 다르게 호출할 수 있게 하는 것.

## Getter, Setter를 사용하는 이유

멤버변수에 직접접근하지 못하게 private으로 접근지정자를 설정하고 public으로 getter, setter 메서드를 만드는 것을 많이 해왔다.

그 이유는 getter, setter를 사용하면 메서드를 통해서 접근하기 때문에, 메서드 안에서 매개변수같이 어떤 올바르지 않은 입력에 대해 사전에 처리할 수 있게 제한하거나 조절할 수 있기 때문이다.

예를들면 setter에서 유효범위를 넘은 정수가 들어왔을 때의 처리를 하고나서 set하거나 예외처리를 해버릴 수 있는 것이다. getter도 마찬가지로 굳이 예를들자면 자료에 무언가 더하거나 빼고 준다든지가 가능하다.

## 객체지향의 설계원칙

- SRP - 단일 책임 원칙 : 한 클래스는 하나의 책임만 가져야 한다.

- OCP - 개방-폐쇄 원칙 : 확장에는 열려있고, 수정에는 닫혀있어야 한다.

- LSP - 리스코프 치환 원칙 : 하위 타입은 항상 상위 타입을 대체 할 수 있어야 한다.

- ISP - 인터페이스 분리 원칙 : 인터페이스 내에 메소드는 최소한 일수록 좋다. (하나의 일반적인 인터페이스보다 여러 개의 구체적인 인터페이스가 낫다.) SRP와 같은 문제에 대한 두 가지 다른 해결책이다.
- DIP - 의존관계 역전 원칙 : 구체적인 클래스보다 상위 클래스, 인터페이스, 추상클래스와 같이 변하지 않을 가능성이 높은 클래스와 관계를 맺어라. DIP 원칙을 따르는 가장 인기 있는 방법은 의존성 주입(DI)이다.

## 예상 질문

- 객체 지향 프로그래밍(OOP)이 뭔가요?
- 객체 지향 프로그래밍의 장, 단점 간단하게 설명해주세요
- 클래스와 인스턴스(객체)는 무엇인지 설명해주세요.
- 객체 지향 프로그래밍에서 추상화 (자료의 추상화)는 무엇인가요?
- 캡슐화가 무엇인가요?
- 상속은 무엇인가요?
- 다형성은 무엇인가요?
- getter와 setter를 사용하는 이유는 무엇인가요?
- 객체지향의 설계원칙에 대해 설명해주세요.

## 참고 링크

https://jeong-pro.tistory.com/95  
https://dev-coco.tistory.com/153
