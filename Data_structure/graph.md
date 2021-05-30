# Graph 자료구조

- 가장 복잡(일반적)한 자료구조
- G = (V,E)
  - V - vertex set (정점 set) (Node개념)
  - E - edge set (link개념) -> {(1,2), (3,4)} ... -> 각 vertex를 잇는 순서쌍

### Graph에 등장하는 용어

<img src="../images/graphDS.jpg" height="50%" width="50%"/>

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

<img src="../images/graph_matrix.png" height="50%" width="50%"/>

- graph A

  - 대각행렬은 각 노드 스스로에 대한 경로를 표현 (1->1) : 0또는 1로 일관성 있게 표현하면 됨
  - 무방향 그래프를 전제하에, 대각원소 기준 인접행렬은 대칭적으로 나타난다.
  - (1,2)원소값 -> 1 -> 1노드와 2노드 사이에 edge가 존재한다는 뜻
  - 1과 0값은 노드들 간의 edge 유무를 표현

- directed graph의 경우
  - 노드 스스로에게 edge 부여하는 값 제외하고 edge의 값에 가중치를 부여하여 표현 (weight value), 가중치는 임의의 값

#### 인접 리스트로 나타내기

- 인접 행렬의 경우 무방향 그래프에서 대칭 edge의 표현에 있어서 데이터 낭비가 존재함.

<img src="../images/graph_list.png" height="50%" width="50%"/>

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
