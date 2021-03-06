# 최단경로 문제 - Ballman Ford & Dijkstra Algorithm

-   dist\[v\] = s에서 v로 가는 최단경로 길이
    -   v 바로 이전의 노드를 u1, u2, u3라고 가정하면,
    -   dist\[v\] = min(dist\[u1\] + weight(u1,v) , dist\[u2\] + weight(u2,v) , dist\[u3\] + weight(u3, v))
    -   weight는 특정 노드로 가는 데에 드는 비용 (edge 값)
    -   이미 저장되어있던 dist\[v\]값이 새로운 경로의 값보다 크면, 이를 수정해주어야함

```python
if dist[v] > dist[u] + w(u,v):
    dist[v] = dist[u] + w(u,v) # 이를 relax(u,v) 작업이라고 함.
```

-   n은 u~v까지 정점의 개수

```python
# Bellman-Ford Algorithm
# Graph G = (V, E) with edges of (possibly negative) costs
def Bellamn-Ford(G = (V, E)):
	# n = number of nodes, m = number of edges
	d = [inf, ..., inf], d[s] = 0
	for i in range(1, n):  # total (n-1) rounds
		for each edge e = (u, v):
			relax(u, v)

	return d
```

-   [bellman Ford Algorithm](https://www.youtube.com/watch?v=FtN3BYH2Zes)

*   u~v까지 각 라운드에 정점의 값을 수정하는 상황
    -   한 라운드에 정점이 갖는 모든 경우의 수를 따져서 값을 완벽히 수정하는 것이 아님.
    -   u~v의 중간 노드인 n1이 존재한다고 가정하면, k라운드에서의 n1값이 수정되었다고 해서 k라운드에 이미 릴랙싱이 끝난 n2 노드 (n1 이후의 노드라고 가정)의 값을 다시 릴랙싱 하지 않는다.
    -   정점의 개수 n개일때, n-1 라운드 만큼 릴랙싱을 해야 모든 경우의 수에 따라서 모든 노드의 릴랙싱을 마치게 됨
*   (n-1) \* Edge = O(nE) = O(n^3)

### Dijkstra

-   bellman-ford 알고리즘의 단점은 어떤 노드에서 릴랙스를 해야하는 지 모르기 때문에 vertex-1만큼, n-1만큼 라운드를 진행하며 릴랙싱을 해야함

```python
def Dijkstra(G):
    n, m = numbers of nodes and edges of G
		s = source node, simply 0
    d = [0, inf, ..., inf]
    parent = [0, NULL, ..., NULL]
    H = make_heap(nodes v of G with key d[v])
    while len(H): # n iterations
        u = H.deleteMin()
        for each v adjacent to u: # m edges are scanned in total
            if (u, v) is an edge of G:
                if d[u] + cost(u, v) < d[v]:
                    d[v] = d[u] + cost(u, v)
                    parent[v] = u
                    H.decreaseKey(v, d[v])
    return dist, parent
```

-   구현 주안점?

    -   for each node u->v상황에서, v노드가 이미 방문한 노드라는 표시

-   decreaseKey -> 노드의 distance값을 저장하는 힙에, 입력된 d\[v\]값을 재배치
-   노드의 distance값을 저장하는 데에는 min_heap을 사용

-   **수행시간**

    1. 모든 노드 v는 min_heap에 한번씩 insert & delete된다. -> O(nlogn)
    2. 모든 edge는 한번의 relax를 함 -> decreaseKey를 한번씩 하게됨. -> decreaseKey는 heapify_up과 수행시간이 같음 O(logn) => O(Elogn) = O(n^2\*logn)

-   최종적으로 parent 관계를 확립해놓으면, 특정노드~노드로까지의 최단경로는 부모 노드로 그려진 트리를 따라가면됨
