# 스택(stack)

- Last In First Out (LIFO, 후입선출) - 나중에 들어간 원소가 먼저 나온다
- 맨 위의 요소를 top으로 가리킴. 삽입 및 삭제 시 top이 가리키는 데이터를 처리
- 시간복잡도 O(1)

## 활용 예시

- 함수의 콜스택, 문자열 역순 출력, 연산자 후위표기법, 웹 브라우저 뒤로 가기, 실행 취소

## 장점

- 구현이 간단하고 데이터 관리에 용이함

## 단점

- 스택의 크기가 정해져있는 경우 오버플로우(Overflow) 또는 언더플로우(Underflow)가 발생할 수 있음. 오버플로우는 가득 찼을 때 데이터를 삽입하는 경우이고 언더플로우는 비어있을 때 데이터를 꺼내는 경우임.  
  => 동적 배열 스택 또는 연결 리스트(Linked List)로 해결 가능

## 코드

```
public class Stack {
    private static int MAX_STACK_SIZE = 10;
    private int top;
    private int[] data = new int[MAX_STACK_SIZE];

    public Stack() {
        top = -1;
    }

    public void push(int data_) throws Exception {
        if (isFull()) {
            throw new Exception("스택이 가득 찼습니다.");
        }
        data[++top] = data_;
    }

    public int pop() throws Exception {
        if (isEmpty()) {
            throw new Exception("스택이 비었습니다.");
        }
        return data[top--];
    }

    public int peek() throws Exception {
        if (isEmpty()) {
            throw new Exception("스택이 비었습니다.");
        }
        return data[top];
    }

    public boolean isEmpty() {
        return top == -1;
    }

    public boolean isFull() {
        return top == MAX_STACK_SIZE - 1;
    }

    public int size() {
        return top + 1;
    }
}
```

## 예상 질문

- Stack의 구조에 대해 설명해주세요.
- tack의 실사용 예를 들어 간단히 설명해주세요.
- Stack 클래스를 손코딩으로 구현해주세요.

## 참고 링크

https://velog.io/@deannn/CS-%EA%B8%B0%EC%B4%88-%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-Stack-Queue
https://velog.io/@kor-seonwoo/CS-%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EC%8A%A4%ED%83%9D  
https://dev-coco.tistory.com/159
