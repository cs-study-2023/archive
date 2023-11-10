# AVL Tree

> Adelson-Velsky and Landis 발명가 이름에서 따왔다.

## 개념정리

### 정의

- 스스로 균형을 잡는 이진 탐색 트리
- 트리의 높이가 h일때 시간복잡도는 O(h)이다. 한쪽으로 치우친 편향 이진트리가 되면 트리의 높이가 높아지면서 시간복잡도가 커지기때문에 이를 방지하고자 높이 균형을 유지하는 AVL 트리를 사용한다.

### 특징

- AVL 트리는 이진 탐색 트리의 속성을 가진다.
- 왼쪽, 오른쪽 서브 트리의 높이 차이가 최대 1이다.
- 어떤 시점에서 높이 차이가 1보다 커지면 회전(rotation)을 통해 균형을 잡아 높이 차이를 줄인다.
- AVL 트리는 높이를 logN으로 유지하기 때문에 삽입, 검색, 삭제의 시간 복잡도는 O(logN)

### Balance Factor(BF)

- Balance Factor = (왼쪽 서브트리 높이) - (오른쪽 서브트리 높이)
- 예시
  - BF가 1이면 왼쪽 서브트리가 오른쪽 서브트리보다 높이가 한단계 높다는 것을 의미
  - BF가 -1이면 왼쪽 서브트리가 오른쪽 서브트리보다 높이가 한단계 낮다는 것을 의미

### 회전(rotation)

- AVL트리는 이진 탐색 트리이기 때문에 모든 작업은 이진 탐색 트리에서 사용하는 방식으로 수행한다.
- 검색 및 순회 연산은 BF를 변경하지 않지만 삽입 및 삭제에서는 BF가 변경될 수 있다.
- **삽입 삭제 시 불균형 상태가 되면 AVL 트리는 불균형 노드를 기준으로 서브트리 위치를 변경한는 rotation 작업을 통해 트리의 균형을 맞춘다.**
  - 불균형 상태는 BF가 -1, 0, 1이 아닌 경우를 말한다.

### 불균형 종류

- 노드들의 배열에 따라 4가지 불균형이 발생하고 이에 따라 rotation 방향을 달리해 트리의 규녕을 맞춘다.

#### LL(Left Left) case

- BF가 2이상인 상황(왼쪽 서브트리 높이가 더 큰 상황)
- right rotation 수행 - y노드의 오른쪽 자식 노드를 z노드로 변경 - z노드 왼쪽 자식 노드를 y노드 오른쪽 서브트리(T2)로 변경 - y는 새로운 루트 노드
  ![AVL_LL](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbiiR2r%2FbtrJUY5baM4%2FyUDa0wduJaJ4pmL0glLMl1%2Fimg.png)

#### RR(Right Right) case

- BF가 -2이하인 상황(오른쪽 서브트리 높이가 더 큰 상황)
- left rotation 수행 - y노드의 왼쪽 자식 노드를 z노드로 변경 - z노드 오른쪽 자식 노드를 y노드 왼쪽 서브트리(T2)로 변경 - y는 새로운 루트 노드
  ![AVL_RR](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FMgydF%2Fbtq2ZpcT9dF%2FWNzhK8Ka9KmiuX6iqj5Ws0%2Fimg.png)

#### LR(Left Right) case

- 왼쪽 자식 노드의 오른쪽 자식 노드때문에 불균형트리인 경우
- left, right 순으로 총 두 번의 rotation을 수행해 균형을 맞춘다.
  ![AVL_LR](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbqqYJK%2FbtrTfOfWWBd%2FKVynhLISaSx98MoUoNORY1%2Fimg.png)

#### RL(Right Left) case

- 오른쪽 자식 노드의 왼쪽 자식 노드때문에 불균형트리인 경우
- right, left 순으로 총 두 번의 rotation을 수행해 균형을 맞춘다.
  ![AVL_RL](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbrTQV1%2Fbtq2TcMbXA3%2FmhrY8bPspDrRT90kkGDIR1%2Fimg.png)

### 결론

> AVL 트리는 이진 탐색 트리의 한 종류로, 편향 트리의 한계점을 보안하기 위해 고안된 균형 트리입니다. 회전을 통해 양쪽 서브 트리의 높이 차이가 2 이상이 되지 않도록 균형을 맞춥니다. 따라서 AVL 트리의 탐색, 삽입, 삭제 수행 시간 복잡도는 O(logN)이 됩니다. 균형을 맞출 때 상황에 따라 다른 회전을 수행합니다.

## 예상 질문

균형 트리 종류는 무엇이 있고 이에대해 설명해주세요.

---

### 참고자료

[[자료구조] AVL 트리(Tree)](https://yoongrammer.tistory.com/72)<br>
[[자료구조] AVL Tree](https://velog.io/@srkim1228/%EA%B8%B0%EC%88%A0%EB%A9%B4%EC%A0%91%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-AVL-Tree)
