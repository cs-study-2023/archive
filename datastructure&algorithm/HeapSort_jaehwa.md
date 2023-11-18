### 힙 정렬

- 힙 정렬은 주어진 배열을 최대 힙 또는 최소 힙으로 구성한 후, 루트 노드를 반복적으로 제거하여 정렬하는 알고리즘입니다.
- 최소 힙의 경우는 오름차순으로 정렬하고, 최대 힙의 경우는 내림차순으로 정렬합니다.
- 최소 힙을 만드는 과정의 시간 복잡도는 logN이기 때문에 heapify 과정을 N번 반복하게 되면 시간 복잡도는 NlogN 이 된다.

**예상 질문**

- 힙 정렬의 과정을 말해주세요.
- 힙정렬 시간복잡도가 어떻게 되는지와 그러한 복잡도가 나오는 이유를 말해주세요.