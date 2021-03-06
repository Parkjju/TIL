# Graph 자료구조

- 가장 복잡(일반적)한 자료구조
- G = (V,E)
  - V - vertex set (정점 set) (Node개념)
  - E - edge set (link개념) -> {(1,2), (3,4)} ... -> 각 vertex를 잇는 순서쌍

### Graph에 등장하는 용어

<img src="images/graphDS.jpg" height="50%" width="50%"/>

1. vertex(정점) or Node
2. 두 노드 또는 정점을 잇는 선 -> edge or link
3. degree (분지수) -> 노드에 인접한 노드의 개수
   - 그래프 G의 분지수 -> 가장 큰 분지수를 가진 노드의 degree값
4. 인접 (adjacent vs incident)
   - e = edge(4,5) -> 4 노드와 5노드는 인접하다.(adjacent)
   - edge e는 노드 4와 노드 5와 인접하다. (incident)
5. 경로(path)
   - 노드 A~B까지 가능 동안 거치는 노드들
   - 거쳐가는 노드는 중복되면 안됨 (3 -> 2 -> 5), (3 -> 2 -> 1 -> 2 -> 5 X)
6. 사이클(cycle)
   - 처음과 끝이 같은 경로 (닫힌 경로), (3 -> 2 -> 5 -> 4 -> 3)
   - cycle이 없는 그래프 : Tree - 트리는 두 노드를 연결하는 경로가 하나밖에 없는 그래프

### Graph의 표현

- 인접성을 표현해야함

- 표현법 1. 인접행렬 (adjacency matrix)
- 표현법 2. 인접 리스트 (adjacency list) -> 리스트는 연결 리스트

- undirected graph(무방향 그래프) - 그래프의 edge에 방향이 없음
- directed graph(방향 그래프) - 그래프의 edge에 방향이 존재하여 노드간 이동이 제한될 수 있음

#### 인접행렬로 나타내기

- n개의 노드가 존재하면, nXn 행렬을 생성한다.

<img src="images/graph_matrix.png" height="50%" width="50%"/>

- graph A

  - 대각행렬은 각 노드 스스로에 대한 경로를 표현 (1->1) : 0또는 1로 일관성 있게 표현하면 됨
  - 무방향 그래프를 전제하에, 대각원소 기준 인접행렬은 대칭적으로 나타난다.
  - (1,2)원소값 -> 1 -> 1노드와 2노드 사이에 edge가 존재한다는 뜻
  - 1과 0값은 노드들 간의 edge 유무를 표현

- directed graph의 경우
  - 노드 스스로에게 edge 부여하는 값 제외하고 edge의 값에 가중치를 부여하여 표현 (weight value), 가중치는 임의의 값

#### 인접 리스트로 나타내기

- 인접 행렬의 경우 무방향 그래프에서 대칭 edge의 표현에 있어서 데이터 낭비가 존재함.

<img src="images/graph_list.png" height="50%" width="50%"/>

- 그림 참고

  - 1노드의 edge (1,2), (1,3), (1,4)...
  - edge표현은 순서에 구애 받지 않음 - (1,3), (1,4), (1,2)로도 표현 가능
  - 각 노드 스스로에게 edge를 부여 -> 일관성있게 진행하면 됨

- directed graph의 경우
  - 인접행렬과 마찬가지로 edge표현에 가중치를 두어 표현
  - 1 -> \[2\] edge가 존재 => 1 -> \[2, weightValue\]

### 그래프 기본연산

- G = (V,E), |V| = n, |E| = m

#### 인접행렬

1. memory : O(n^2)
2. e = (u,v)가 존재하는가?
   - if G\[u\]\[v\] == 1로 찾기 -> O(1)
3. u에 인접한 모든 노드 v에 대한 특정연산 -> O(n), 각 노드에 대한 edge 유무 판단을 위해 모든 노드의 edge값을 검사해야함.

```python
#pseudo code
for v in range(1,n+1):
    do with G[u][v]
```

4. new edge(u,v) 삽입 -> G\[u\]\[v\] = 1 -> O(1)
5. edge(u,v) 삭제 -> G\[u\]\[v\] = 0 대입 -> O(1)

#### 인접리스트

1. memory : O(n+m)
2. G\[u\].search(v) - G\[u\]는 인접리스트
   - 최악의 경우 노드 u 스스로를 제외하고 u가 모든 노드와 연결되어 있는 상태 -> worst case - search가 O(n)
3. u에 인접한 모든 노드 v에 대한 특정연산 -> O(인접한 노드의 수) - worst case의 경우 O(n)

```python
#pseudo code
for each edge in G[u]:
    do something
```

4. new edge(u,v)삽입 -> G\[u\].pushFront(v) -> O(1)
5. edge(u,v) 삭제
   - x = G\[u\].search(v)
   - G\[u\].remove(x)
   - 최악의 경우 search에 O(n)시간 발생

- 인접행렬과 인접리스트의 비교
  - 연산 자체는 인접행렬이 효율적인 부분이 더 많음
  - 결정적으로 그래프 자체가 차지하는 메모리의 크기가 인접리스트가 더 좋음
  - n개의 노드에 비해 edge의 수인 m값이 상대적으로 작으면 **sparse라고 표현**
  - **dense**의 경우는 edge의 개수가 n과 비교하여 큰 상황

* 참고 - python의 리스트로 인접리스트를 구현하려면 순서에 구애받지 않기 위해 append함수를 사용해야함!!!!

## 그래프 순회 (Graph Traversal) : DFS(Depth First Search)

- 그래프의 순회 방법
  1. DFS (깊이 우선 탐색)
  2. BFS (너비 우선 탐색)

1. DFS

   - 알파벳을 노드의 값으로 갖는 graph가 존재한다고 가정.
   - a와 인접한 노드들 중 특정 기준을 만들어 먼저 search할 노드를 선택하여 진행 (알파벳 사전편찬 순으로 진행한다고 가정)
   - a와 b,c노드가 인접했다고 가정하면 a->b로 서치
   - b에서 다시 b와 인접한 여러 노드들 중 기준에 맞으면서 search하지 않은 노드로 진행
   - 끝까지 가서 더 이상 search할 노드가 존재하지 않으면 backtrack으로 search를 시작한 노드까지 이동
   - backtrack은 역추적 진행하다가 인접한 노드들 중 search하지 않은 노드가 존재할 때 역추적 그만두고 다시 해당 인접노드로 search를 진행

2. BFS
   - a와 인접한 노드 b,c가 있으면, 해당 노드들을 모두 search한 뒤에 다음 레벨로 넘어가는 방식
   - 모든 형제 노드들을 search

### DFS순회방법

<img src="images/DFS.png" height="50%" width="50%" />

- a에서 DFS로 순회

  - a -> b -> c -> d -> f 이후 backtrack -> b까지 옴
  - b -> e -> g 이후 backtrack
  - b -> h 이후 backtrack하여 a까지 이동

- code구현 -> recursive case

```python
#pseudo code
global currentTime = 1

def DFS(v):
    mark[v] = "visited"
    pre[v] = currentTime # pre[v]는 v의 첫번째 방문 시간
    currentTime += 1
    for each edge(v,w): # v에 인접한 모든 노드 w에 대해
        if mark[w] != "visited":
            parent[w] = v
            DFS(w)
    # v에 인접한 모든 노드를 고려한 상태이기 때문에 for loop를 탈출함
    post[v] = currentTime # v에서 인접한 모든 노드를 방문 완료한 순간, v에서 DFS가 완료된 시간
    currentTime+=1
    # return

def DFSALL(G): #그래프 G의 컴포넌트가 떨어져 있는 상황도 있음
    for all nodes in G:
        mark[v] = "unvisited"
    for all nodes v:
        if mark[v] != "visited":
            DFS(v)
```

- DFS 함수 정의에 따라 도식화한 그림 -> Tree형태를 띰. -> DFS Tree (parent리스트를 통해 도식화)

- pre,post time & parent list가 핵심
- 추가적으로 DFSALL(G) : #graph G를 DFS search

- code 구현 -> non recursive case
  - 비재귀적 구현에서는 stack이 등장
  - currentTime, pre&post time 정의는 직접 추가 필요

```python
def DFS(s):
    stack.push((∅, s)) # ∅는 부모노드, s는 현재 방문노드
    while stack is not empty:
        p, v = stack.pop() # tuple형태로 stack에 저장하기 때문에 unpacking하여 p,v에 저장
        if v is unmarked:
            mark[v] = "visited"
            parent[v] = p
            for each edge(v,w):
                if w is unmarked:
                    stack.push((v,w)) # push또한 저장 기준에 입각하여 진행 - 사전편찬 순으로...예시
                    # 먼저 방문이 진행되는 노드가 top에 오도록 push
```

- DFS tree의 경우 본 그래프에서 나타났던 모든 edge가 표기되지 않을 수 있음.

  - DFS에서 나타나지 않은 edge -> back edge

- back edge존재 의미
  - ex) DFS 이미지에서 c - f - d 트리에서 f -> c로의 back edge가 존재
  - c - f - d 로 구성되는 cycle이 존재한다는 뜻.

<img src="images/DFStree.png" height="30%" width="60%"/>

- pretime~post time 구간의 포함관계가 DFS tree를 구성한다.

### DAG (Directed Acyclic Graph) : 사이클이 없는 방향 그래프

- 선후 관계에 따라 상위노드로부터 데이터를 받는데, 하위 노드의 입장에서 자신의 모든 상위 노드가 일련의 처리 과정을 마쳐 자신에게 특정 데이터를 전달해주고 나서야 자신도 상위 입장의 노드가 되어 하위 노드에게 데이터 처리를 시작할 수 있게 된다.

<img src="images/topological.png" height="50%" width="50%"/>

- 선후 관계에 따라 일의 순서를 결정 -> topological sorting(위상정렬)
- post time값이 가장 작은 값 -> 가장 먼저 처리가 끝나는 노드
  - incoming만 있고 outgoing은 없는 노드.
  - 위상정렬에 따라 가장 마지막에 위치해야함.
  - 이후 post time 비교하며 차례로 배열 (post time가장 큰 값을 가진 노드가 가장 처음에 위치해야함)
