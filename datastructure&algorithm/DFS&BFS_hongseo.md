# DFS & BFS

> Depth - First Search & Breadth - First Search

## 개념정리

- DFS와 BFS 모두 하나의 정점으로부터 시작해 차례로 모든 정점들을 방문하는 알고리즘이다.

### DFS(깊이 우선 탐색)

- 정의
  - 갈 수 있는 만큼 최대한 깊이 탐색한 후 더이상 갈곳이 없으면 이전 정점으로 돌아가는 탐색 방법이다.
  - **모든 노드**를 방문하고자 할 때, 이 방법을 선택
  - ![dfs](https://blog.kakaocdn.net/dn/TJafT/btq53RxBHk6/l5ZyDuc4WR7y4Dz4xLku2k/img.gif)
- 구현방법

  - 자기 자신을 호출하는 순환 알고리즘 형태이다.(재귀 or 스택)

  ```java
  	// dfs, 재귀, 인접 행렬, i 정점부터 시작한다.
      public static void dfs(int i) {
          visit[i] = true; // 노드 중복 접근 방지를 위한 방문 체크 배열. (boolean)
          System.out.print(i + " ");// j는 dfs 배열의 새로운 분기를 뜻한다(int)
          for(int j=1; j<n+1; j++) {
              if(map[i][j] == 1 && visit[j] == false) {
  				dfs(j);
              }
  		}
      }
  ```

  ```java
  public void dfs_stack(int startNode, int[][] graph) {
      boolean[] visited = new boolean[n];

      Stack<Integer> stack = new Stack<>();
      stack.push(startNode);

      while(stack.empty() == false) {
          int currentNode = stack.pop();

          if(visited[currentNode]) {
              continue;
          }

          visited[currentNode] = true;
          System.out.println(currentNode + "방문");
          for(int next = 0; next < n; next++) {
              if(visited[next] == false && graph[currentNode][next] != 0) {
                  stack.push(next);
              }
          }
      }
  }
  ```

- 장점
  - 현 경로상의 노드들만 기억하면 되므로 저장공간 수요가 비교적 적다.
  - 목표 노드가 깊은 단계에 있을 경우 해를 빨리 구할 수 있다.
- 단점
  - 해가 없는 경로가 깊을 경우 탐색시간이 오래 걸릴 수 있다.
  - 얻어진 해가 최단 경로가 된다는 보장이 없다.
  - 깊이가 무한히 깊어지면 스택오버플로우가 날 위험이 있다. (깊이 제한을 두는 방법으로 해결가능)

### BFS(넓이 우선 탐색)

- 정의

  - 인접 노드를 먼저 탐색하는 방법이다.
  - DFS와는 정반대로 가로로 한줄씩 읽는다고 생각하면 된다.
  - ![bfs](https://blog.kakaocdn.net/dn/ddKphh/btq52wHI45p/1LkoIejc0b50lbvV8aAlX0/img.gif)

- 구현 방법
  - BFS는 방문한 노드들을 차례로 저장한 후 꺼낼 수 있는 자료 구조인 **Queue**를 사용
  - 지금 위치에 갈 수 있는 정점을 모두 Queue에 넣는다.
  ```java
  public static void bfs(int i) {
      Queue<Integer> q = new LinkedList<>();
      q.offer(i);
      visit[i] = true; // 노드 중복 접근 방지를 위한 방문 체크 배열.(boolean)
  	while(!q.isEmpty()) {
          int temp = q.poll();
          System.out.print(temp + " ");
          for(int j=1; j<n+1; j++) {
              if(map[temp][j] == 1 && visit[j] == false) {
                  q.offer(j);
                  visit[j] = true;
              }
          }
      }
  }
  ```
- 장점
  - 너비를 우선으로 탐색하므로 답이 되는 경로가 여러 개인 경우에도 최단경로를 얻을 수 있다.
  - 노드 수가 적고 깊이가 얕은 해가 존재할 때 유리하다.
- 단점
  - DFS와 달리 큐를 이용하여 다음에 탐색할 정점들을 저장하므로 더 큰 저장공간이 필요하다.

## 예상 질문

- DFS, BFS의 설명, 차이점

---

### 참고자료

[[JAVA] DFS Stack 구현](https://pcloud.tistory.com/27)<br>
[[알고리즘] 깊이 우선 탐색(DFS)과 너비 우선 탐색(BFS)](https://currygamedev.tistory.com/10)<br>
[[Java] DFS, BFS 정리](https://bbangson.tistory.com/42)<br>
