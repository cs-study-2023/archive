# Binary Tree(이진 트리)

## 개념정리

### Tree(트리)란?

- 트리는 비선형 자료구조로 계층적 관계 표현한다.
- **특징**
  - 노드(Node)들과 노드들을 연결하는 간선(Edge)들로 구성되어 있다.
  - 트리는 하나의 루트 노드를 가진다.
  - 루트 노드는 0개이상의 자식노드를 갖는다.
  - 자식 노드 또한 0개 이상의 자식 노드를 갖는다.
  - 트리는 사이클을 가질 수 없다.
    - ![트리_사이클](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FSTYj3%2Fbtq9HLN0qjh%2F0eYwIozRRGKJhPcfm3KWek%2Fimg.png)
  - 트리 노드는 self-loop가 존재해서는 안된다.
    - ![트리_셀프_루프](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FVS1CM%2Fbtq9E6E89gV%2FalDzlnmFHWShcRa4EAxhSk%2Fimg.png)

### 트리 관련 용어

![트리_관련_용어](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FVw14V%2Fbtq9LqaPkJn%2FGK5HUpRCqgdQ7wqZOKTBkK%2Fimg.png)

- 루트 노드(root node) : 부모가 없는 노드로 트리는 단 하나의 루트 노드를 가진다. (ex : A- 루트노드)
- 단말 노드(leaf node) : 자식이 없는 노드로 terminal 노드라고도 부른다. (ex : C, D, E - 단말 노드)
- 내부 노드(internal node) : 단말 노드가 아닌 노드(ex : A, B - 내부 노드)
- 간선(edge) : 노드를 연결하는 선
- 형제(sibling) : 같은 부모 노드를 갖는 노드들 (ex : D-E, B-C : 형제)
- 노드의 깊이(depth) : 루트 노드에서 어떤 노드에 도달하기 위해 거쳐야 하는 = 간선의 수(ex : D의 depth : 2)
- 노드의 레벨(level) : 트리의 특정 깊이를 가지는 노드의 집합 ( ex : level 1- {B, C} )
- 노드의 차수(degree) : 자식 노드의 개수 (  ex : B의 degree - 2, C의 degree - 0)
- 트리의 차수(degree of tree) : 트리의 최대 차수 ( ex : 위 트리의 차수는 2이다)

### Binary Tree 정의

- 모든 노드들이 둘 이하의 자식을 가진 트리
- 모든 노드의 차수가 2이하
- ![이진트리_이미지](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FblbjFV%2Fbtq1K3P9Y8v%2FH393OwoRI9lX8N3wrz9OO1%2Fimg.png)

## 예상 질문

- BST(Binary Search Tree)와 Binary Tree에 대해 설명해주세요.

---

### 참고자료

[[자료구조] 이진 트리 (Binary tree) 알아보기](https://yoongrammer.tistory.com/69)<br>
[신입 개발자 기술면접 질문 정리 - 자료구조](https://dev-coco.tistory.com/159)<br>
[[자료구조] 트리(Tree)의 개념, 이진 트리, 전 이진 트리, 완전 이진트리, 포화 이진 트리, 이진 탐색트리](https://code-lab1.tistory.com/8)
