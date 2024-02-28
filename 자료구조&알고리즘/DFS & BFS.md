# **DFS & BFS**

그래프를 탐색하는 방법에는 크게 **깊이 우선 탐색(DFS)**과 **너비 우선 탐색(BFS)**이 있습니다.

그래프란, **정점(node)과 그 정점을 연결하는 간선(edge)으로 이루어진 자료구조의 일종**을 말하며,

그래프를 탐색한다는 것은 **하나의 정점으로부터 시작하여 차례대로 모든 정점들을 한 번씩 방문하는 것**을 말합니다.

### **1. 깊이 우선 탐색 (DFS, Depth-First Search)**

### **: 최대한 깊이 내려간 뒤, 더이상 깊이 갈 곳이 없을 경우 옆으로 이동**

![!https://blog.kakaocdn.net/dn/xC9Vq/btqB8n5A25K/GyOf4iwqu8euOyhwtFuyj1/img.gif](https://www.notion.so/image/https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FxC9Vq%2FbtqB8n5A25K%2FGyOf4iwqu8euOyhwtFuyj1%2Fimg.gif?table=block&id=ef6ce6ea-a167-4843-a194-2bd547218a46&spaceId=cdf5fd00-85a4-4001-aa3d-4b52542685d0&userId=ed1d1611-a9cd-4fe1-9eab-44a46191e599&cache=v2)

출처 https://developer-mac.tistory.com/64

### **깊이 우선 탐색의 개념**

루트 노드(혹은 다른 임의의 노드)에서 시작해서 다음 분기(branch)로 넘어가기 전에 **해당 분기를 완벽하게 탐색**하는 방식을 말합니다.

예를 들어, 미로찾기를 할 때 최대한 한 방향으로 갈 수 있을 때까지 쭉 가다가 더 이상 갈 수 없게 되면 다시 가장 가까운 갈림길로 돌아와서 그 갈림길부터 다시 다른 방향으로 탐색을 진행하는 것이 깊이 우선 탐색 방식이라고 할 수 있습니다.

1. 모든 노드를 방문하고자 하는 경우에 이 방법을 선택함

2. 깊이 우선 탐색(DFS)이 너비 우선 탐색(BFS)보다 **좀 더 간단함**

3. 검색 속도 자체는 너비 우선 탐색(BFS)에 비해서 **느림**

### **2. 너비 우선 탐색 (BFS, Breadth-First Search)**

### **: 최대한 넓게 이동한 다음, 더 이상 갈 수 없을 때 아래로 이동**

https://www.notion.so/image/https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc305k7%2FbtqB5E2hI4r%2Fea7vFo08tkDYo4c8wkfVok%2Fimg.gif?table=block&id=f3786bde-f3c6-4193-bfa0-95b928de5b67&spaceId=cdf5fd00-85a4-4001-aa3d-4b52542685d0&userId=ed1d1611-a9cd-4fe1-9eab-44a46191e599&cache=v2

출처 https://developer-mac.tistory.com/64

### **너비 우선 탐색의 개념**

루트 노드(혹은 다른 임의의 노드)에서 시작해서 **인접한 노드를 먼저** **탐색**하는 방법으로, 시작 정점으로부터 가까운 정점을 먼저 방문하고 멀리 떨어져 있는 정점을 나중에 방문하는 순회 방법입니다.

주로 두 노드 사이의 **최단 경로**를 찾고 싶을 때 이 방법을 선택합니다.

ex) 지구 상에 존재하는 모든 친구 관계를 그래프로 표현한 후 Sam과 Eddie사이에 존재하는 경로를 찾는 경우

- 깊이 우선 탐색의 경우 - 모든 친구 관계를 다 살펴봐야 할지도 모름
- 너비 우선 탐색의 경우 - Sam과 가까운 관계부터 탐색

### **3. 깊이 우선 탐색(DFS) 과 너비 우선 탐색(BFS) 비교**

https://www.notion.so/image/https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcQYkI8%2FbtqB8oDsMGe%2FEEYm0cKGYhxTR0kJhGiJPK%2Fimg.gif?table=block&id=80fe1af0-ef5a-4992-a183-bf7f125e292e&spaceId=cdf5fd00-85a4-4001-aa3d-4b52542685d0&userId=ed1d1611-a9cd-4fe1-9eab-44a46191e599&cache=v2

출처 https://namu.wiki/w/BFS

| DFS(깊이우선탐색)                                 | BFS(너비우선탐색)                       |
| ------------------------------------------------- | --------------------------------------- |
| 현재 정점에서 갈 수 있는 점들까지 들어가면서 탐색 | 현재 정점에 연결된 가까운 점들부터 탐색 |
| 스택 또는 재귀함수로 구현                         | 큐를 이용해서 구현                      |

### **DFS와 BFS의 시간복잡도**

두 방식 모두 조건 내의 모든 노드를 검색한다는 점에서 시간 복잡도는 동일합니다.

DFS와 BFS 둘 다 다음 노드가 방문하였는지를 확인하는 시간과 각 노드를 방문하는 시간을 합하면 됩니다.

N은 노드, E는 간선일 때

- 인접 리스트 : O(N+E)
- 인접 행렬 : O(N^2)

일반적으로 E(간선)의 크기가 N²에 비해 상대적으로 적기 때문에 인접 리스트 방식이 효율적임
