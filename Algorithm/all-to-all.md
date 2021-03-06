# All-to-All shortest path problem

- source node로부터 다른 모든 노드로 가는 최단경로
- 방법 1 : 정점 set V안의 모든 노드들에 대해 dijkstra 알고리즘 적용 -> O(nD) -> O(nmlogn) (n은 정점, m은 edge) (m은 n^2까지 증가 가능) -> O(n^3logn)
- greedy + DP, relax는 새로운 최단경로의 값이 나타나면 다시 수정해줘야함

```python
for each node s in V:
    Dijkstra(s)
```

- 방법 2 : DP (Dynamic programming)방법 - Floyd-warshall알고리즘
  - 노드 = {1,2,..., n}
  - O(n^3)
  - 순수 DP로 더 직관적인 이해 가능 (다익스트라는 heap을 사용해야했다)

```python
for i,j in {1,2,...,n}:
    p(i,j)계산 # p(i,j) = 노드 i~ 노드j까지 최단경로
    # or d(i,j)계산 - 값은 P(i,j)와 동일, d는 DP식으로 계산
```

### Floyd-warshall

1. 해(최단경로)를 분석
   - shortPath(i,j) = shortPath(i,k) + shortPath(k,j)
   - d(i,j) = d(i,k) + d(k,j) : DP식. 더 작은 단위로 쪼개는 작업
   - k를 정하는 방법 : i와j사이의 가장 큰 이름을 지닌 노드 (3->1->9->4->6->8, k=9) - P_9(3,8) = P_8(3,9) + P_8(9,8)
   - 일반화) P_n(3,8) = P_n-1(3,n) + P_n-1(n,8)
     P_k(i,j) = 노드i ~ 노드j, i와j사이에 등장하는 노드의 번호는 k이하 = P_k-1(i,k) + P_k-1(k,j)
2. DP 점화식 도출
   - dk(i,j) = d_k-1(i,k) + d_k-1(k,j)
3. 계산
   - d0(i,j) -> i~j까지 가는데, 0보다 작은 노드는 없으므로 i와j가 직접 연결되어있거나 edge가 없으면 weight를 inf로 설정
   - d0(i,i) = 0

- 참고 - dk(i,j) = min(d_k-1(i,j) , d_k-1(i,k) + d_k-1(k,j)) // 엄밀한 기준에서 DP식

  - d_k-1(i,j) -> 노드 k를 통과하지 않는 것이 더 짧은 경로일 경우

- [wiki - floyd warsall alogorithm](https://en.wikipedia.org/wiki/Floyd%E2%80%93Warshall_algorithm)

  - DP table작성. (d0부터 - 직접edge로 연결되어있거나 아니거나)
  - d1(i,j) = min(d0(i,j) , d0(i,1) + d0(i,1))

- pseudo code
  1. d : 2차원 리스트 n X n , 초기값 inf
  2. d 초기화
     - d\[i\]\[j\] = weight(i,j) if (i,j) in E (else inf)
  3. for j = 1 to n : k=1,2,...n (노드 이름) (k for루프이므로 점화식에 적용 됨)
  4. 이중 for루프 -> for(i,j) : d\[i\]\[j\] = min(d\[i\]\[j\], d\[i\]\[k\] + d\[k\]\[j\])
- time -> n^3, memory(space) -> n^2(2차원)
