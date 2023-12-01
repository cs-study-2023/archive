### JVM 이란?

자바 가상 머신(JVM)은 자바 프로그램을 실행하는 환경을 제공하는 소프트웨어이다. 이를 통해 자바 언어로 작성된 프로그램은 운영체제에 독립적인 바이트 코드로 변환되며, JVM은 이 바이트 코드를 해석하고 실행한다. 모든 JVM은 자바 바이트 코드를 실행하는 규격에 따라 동작하며, 이는 운영체제와는 독립적이다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/fb38e82c-61f0-4aa9-b785-e0a798e9b9df/d0dcf82d-beff-468f-ab12-5a453440093f/Untitled.png)

### JAVA 메모리 구조

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/fb38e82c-61f0-4aa9-b785-e0a798e9b9df/754dabaf-a670-4046-9e86-0340f19f0349/Untitled.png)

1. **Class Loader:**
    - 자바 소스 코드는 컴파일되어 .class 파일(바이트 코드)로 생성된다.
    - Class Loader는 이 .class 파일들을 JVM이 실행할 수 있는 형태로 메모리에 적재(로딩)한다.
    - Runtime Data Area로 .class 파일들을 로딩하여 자바 애플리케이션 실행을 위한 준비를 한다.
2. **Execution Engine:**
    - Execution Engine은 메모리에 적재된 바이트 코드를 기계어로 변환하여 실행하는 역할을 한다.
    - 두 가지 주요 방식으로 동작한다:
        - **Interpreter (해석기):** 바이트 코드를 한 줄씩 읽어서 해석하고 실행한다. 대화형식 컴파일 방식.
        - **JIT(Just-In-Time) Compiler:** 전체 바이트 코드를 네이티브 코드로 변환하여 실행하므로 성능이 인터프리터보다 우수하다. 실행 시간에 동적으로 컴파일을 수행한다.
3. **Garbage Collector:**
    - Garbage Collector는 Heap 메모리 영역에 적재된 객체 중에서 참조되지 않는 객체를 탐지하여 제거한다.
    - 객체의 생존 여부를 확인하고 더 이상 사용되지 않는 객체들을 해제하여 메모리를 효율적으로 관리한다.
    - GC가 동작하는 동안 일시적으로 모든 쓰레드가 정지되는데, 이를 GC의 stop-the-world이라고 한다.
4. **Runtime Data Area:**
    - JVM의 메모리 영역으로 자바 애플리케이션을 실행할 때 사용되는 데이터를 저장한다.
    - 크게 다섯 가지 영역으로 구분된다:
        - **Method Area**
            - 클래스 멤버 변수 및 메소드 정보, Constant Pool, type 정보, static 변수, final class 변수 등이 저장되는 영역이다.
            - 클래스가 로드될 때 생성되며, 모든 쓰레드가 공유하는 공간이다.
        
        - **Heap Area**
            - new 키워드로 생성된 객체와 배열이 저장되는 영역이다.
            - 메소드 영역에 로드된 클래스만 생성 가능하며, GC를 통해 참조되지 않는 메모리를 정리한다.
            - JDK 8부터는 permanent 영역이 없어지고, meta space가 추가되었다.
        - **Stack Area**
            - 지역 변수, 파라미터, 리턴 값, 임시 값, 메서드 호출 등의 임시 데이터가 저장되는 영역이다.
            - 정적 메모리 할당이 이루어지는 장소로, Heap 영역에 동적 할당된 값에 대한 참조를 가질 수 있다.
        - **PC Register**
            - 쓰레드가 생성될 때마다 생성되며, 현재 쓰레드가 실행 중인 부분의 주소와 명령을 저장하는 영역이다.
            - 쓰레드 간에 돌아가며 수행할 수 있도록 한다.
        - **Native Method Stack**
            - 자바 외의 언어로 작성된 Native 코드를 위한 메모리 영역이다.
            - 보통 C/C++ 등의 코드를 수행하기 위한 Stack이며, Native 메서드 호출 정보를 저장한다.






**예상 질문**

1. JVM 이란?
2. JVM 메모리 구조에 대해 설명해주세요.
3. 2번에서 꼬리 질문 형식으로..?