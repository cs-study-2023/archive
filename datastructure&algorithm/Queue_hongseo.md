# Queue(큐)

## 개념정리

### 정의

- 큐(Queue)는 한쪽 끝에서만 삽입이 이루어지고, 다른 한쪽 끝에서는 삭제 연산만 이루어지는 유한 순서 리스트이다.
- 가장 큰 특징은 FIFO(First In First Out, 선입선출) 구조라는 것이다.
  - 가장 먼저 들어온 데이터가 가장 먼저 나옴
- ![Queue_이미지](https://raw.githubusercontent.com/Songwonseok/CS-Study/main/DataStructure/images/queue-1.PNG)

### 활용 예시

- 버퍼, 우선순위가 같은 작업 예약, 은행 업무, 콜센터 고객 대기, BFS

### 주요 동작

- enqueue() : 큐에 데이터를 넣는다.
- dequeue() : 큐에서 데이터를 빼낸다.
- isEmpty() : 큐가 비어있는지 확인한다.
- isFull() : 큐가 꽉 차 있는지 확인한다.
- peek() : 앞에있는 원소를 삭제하지 않고 반환한다.

### 구현

- 기본값

```java
private int size = 0;
private int rear = 0;
private int front = 0;

Queue(int size) {
    this.size = size;
    this.queue = new Object[size];
}

```

---

- enqueue: 데이터 넣음

```java
public void enqueue(Object o) {
    if(isFull()) {
        return;
    }
    queue[rear++] = o;
}
```

> - 현재 가장 끝 위치를 가리키는 rear에 값을 넣고 rear를 1 증가시켜 다시 가장 끝 위치를 가리키도록 한다.
> - 가득 찬 상태에서 enqueue를 하면 overflow

---

- dequeue: 데이터 뺌

```java
public Object dequeue(Object o) {

    if(isEmpty()) {
        return null;
    }
    Object o = queue[front];
    queue[front++] = null;
    return o;
}
```

> - 현재 가장 앞 위치를 가리키는 front에 위치한 값을 꺼낸 후, 해당 위치에 null 삽입한다. front를 증가시켜 다시 가장 앞 위치를 가리키도록 한다.
> - queue가 빈 상태에서 dequeue를 하면 underflow

---

- isEmpty: 비어있는지 확인

```java
public boolean isEmpty() {
    return front == rear;
}
```

> - front와 rear가 같으면, 가장 앞 원소 위치와 가장 끝 원소 위치가 같은 것으로 비어있다고 판단

---

- isFull: 꽉차있는지 확인

```java
public boolean isFull() {
    return (rear == size-1);
}
```

> - rear가 사이즈 - 1과 같으면 가득 찬 것이다.

### 단점

- front와 rear를 뒤로 움직이면서 데이터 저장
- 큐에 빈 메모리가 남아있어도, rear가 끝을 가리키면 꽉 차있다고 판단
- 이를 개선하더라도 다음 인덱스 데이터를 모두 앞으로 한칸 이동하는 시간이 필요함(O(N))

### 원형 큐

- 일반 큐의 단점을 개선
- 논리적으로 배열의 처음과 끝이 연결되어 있다고 간주
- ![원형큐_이미지](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FVmXHm%2FbtqPKt5ZRW2%2FyEmLiSotBcgJU3UflwMAb1%2Fimg.png)

### 원형 큐 구현

- enqueue

```java
public void enqueue(Object o) {

    if(isFull()) {
        return;
    }

    rear = (++rear) % size;
    queue[rear] = o;
}
```

---

```java
public Object dequeue() {

    if(isEmpty()) {
        return null;
    }

    front = (++front) % size;
    return queue[front];
}
```

---

```java
public boolean isFull() {
    return ((rear+1) % size == front);
}
```

### 원형큐 단점

- 배열을 사용해서 구현되기때문에 큐의 크기가 제한된다.
- 배열 크기를 직접 줄이거나 늘려줘야한다.
- 구현이 복잡하다.

### 연결리스트 큐

- 원형큐의 단점 개한다.
- 각 데이터들을 노드(node) 객체에 담고 노드 간 서로 연결하는 방식으로 구현
- 배열 크기를 직접 관리할 필요 없고 삽입, 삭제때 링크를 연결하거나 끊어주기만 하면 된다. -![연결리스트_큐_이미지](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbz4A3X%2FbtqPDIJaMsJ%2FEqGrydOR2k5zwE1mvWZC1K%2Fimg.png)

### 연결리스트 구현

![연결리스트_큐_offer](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F3LfGv%2FbtqPwmtPgBI%2FvQSLQg4K4UUO4Y5vdIP7IK%2Fimg.png)
![연결리스트_큐_poll](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbp8Hly%2FbtqPC0wu8Gi%2FFQ5TpL5QlG6m6VKk3OWQA0%2Fimg.png)

```java
class Node<E> {
    E data;
    Node<E> next; //다음 노드를 가리키는 역할

    Node(E data) {
        this.data = data;
        this.next = null;
    }
}

public class LinkedListQueue<E> {
    private Node<E> head;
    private Node<E> tail;
    private int size;

    public LinkedListQueue() {
        this.head = null;
        this.tail = null;
        this.size = 0;
    }

    public boolean offer(E value) {
        Node<E> newNode = new Node<E>(value);

        if(size == 0) { //비어있으면, head에 삽입
            head = newNode;
        } else { // 그 외의 경우 마지막 노드(tail)의 다음 노드(next)가 새 노드를 가리키도록 한다.
            tail.next =  newNode;
        }

        // tail을 새로 입력한 노드로 변경
        tail = newNode;
        size++;

        return true;
    }
    public E poll() {
        if(size == 0) { //비어있으면, 삭제할 노드 없으므로 null 반환
            return null;
        }

        //삭제할 요소의 데이터 반환위한 임시변수(temp)
        E element = head.data;
        Node<E> nextNode = head.next;

        //head 모든 데이터 삭제
        head.data = null;
        head.next = null;

        //head가 가리키는 노드를 삭제된 head노드의 다음노드 가리키도록 변경
        head = nextNode;
        size--;

        return element;
    }
}

```

## 예상질문

- 스택과 큐에 대해서 설명해 주세요.
- 스택과 큐의 실사용 예를 들어 간단히 설명해주세요.
- Priority Queue(우선순위 큐)에 대해 설명해주세요.

---

### 참고자료

[[자료구조]원형 큐(Circular queue)](https://bambbang00.tistory.com/5)<br>
[[자료구조] 큐(Queue) 란? 한번에 쉽고 간단하게 이해하기!](https://donggu1105.tistory.com/163)<br>
[CS-Study/DataStructure
/Stack & Queue.md](https://github.com/Songwonseok/CS-Study/blob/main/DataStructure/Stack%20%26%20Queue.md)<br>
[자바 [JAVA] - 연결리스트를 이용한 Queue (큐) 구현하기](https://st-lab.tistory.com/184)<br>
[신입 개발자 기술면접 질문 정리 - 자료구조](https://dev-coco.tistory.com/159)<br>
