# heap 정의

### 힙 성질을 만족하는 이진트리

-   n개의 노드로 이루어진 이진트리 중 높이가 제일 작은 트리

*   리스트 H=[ a,b,c,None,d,e,f ] -> 자식노드가 없어도 공간을 차지한다고 생각.

    -   H\[0\]의 왼쪽 자식노드 => H\[1\]
    -   H\[2\]의 오른쪽 자식 노드 => H\[2\*2+2\] (왼쪽 자식노드는 + 1)

*   일반화
    -   H\[k\]의 왼쪽 자식노드 : H\[2\*k+1\]
    -   H\[k\]의 오른쪽 자식노드 : H\[2\*k+2\]
    -   H\[k\]의 부모노드 : H\[(k-1)//2\]
*   결론적으로, **자식노드와 부모노드를 상수시간에 계산해낼 수 있다**
*   단점) 3레벨의 자식노드들이 최 우측단 노드밖에 없다고 가정 -> 불필요한 메모리를 낭비하게 됨.

**Heap 성질이란?**

-   모든 부모노드의 key값은 자식 노드의 key 값보다 작지 않다.

-   예) A=\[2,8,6,1,10,15,3,12,11\] -> 부모노드 2는 자식노드의 key보다 작음.

1. 모양 -> 리스트 표현법에서 좌측부터 끝까지 꽉 채워져 있는 상태(**완전 이진트리** -> 오른쪽 자식노드부터 제거되었다고 가정하는 트리)
2. heap성질 만족

-   리스트의 표현법을 트리로 해석하였을때 위의 두 조건을 만족하면 heap이다.

-   **도출해낼 수 있는 결론**

    -   루트노드 -> max-value, index-0 value

-   구현하는 연산
    1. insert 연산 O(logn)
    2. find_max 연산 - return root_node (O(1))
    3. delete_max 연산 O(logn) -> **지우고 남은 노드들도 heap성질도 만족해야함!!!! - 적당한 배치 필요**

### make_heap 연산

-   A = \[2,8,6,1,10,15,3,12,11\] 트리 (재배치를 통해 heap으로 만드는 연산이 make_heap연산)
-   **heapify-down**연산 구현이 우선되어야 함.
    1. leaf노드를 연산에서 무시
    2. 특정 노드의 자식 노드에 대해 *2+1, *2+2 연산을 통해 key값을 비교하여 **부모 노드가 자식노드보다 작으면, 자식노드들 중에 더 큰 값으로 위치를 바꾼다**
    3. 2번과정을 마치면 작은heap이 완성된 것.
    4. 우측에서 좌측으로 순회하며 2번 과정을 계속해서 반복하다가, **자식 노드와 바꾼 뒤에도 자식의 자식 노드보다 key값이 작으면 자식의 자식 노드와도 자리를 바꿔줘야함** -> 자식노드가 leaf일때까지.
    5. 루트까지 마무리하면, 전체 heap이 만들어짐.

```text
# pseudo code
make_heap(A):
    n = len(A)
    for k in range(n-1, -1, -1):
        # A[k] -> heap 성질 만족하는 곳으로
        heapify_down(k,n) # k-> A[k], heap원소의 갯수

heapify_down(k,n):
    # A[k]를 제자리로, n개의 원소를 지닌 트리
    while A[k] != leaf_node:
        L,R = 2*k+1, 2*k+2
        m = max_index(A[k],A[L], A[k])

        if k!=m: # maximum이 L이나 R이라는 뜻, 자식노드의 키값이 더 크다는 뜻
            A[k],A[m] = A[m],A[k]
            k=m
        else:
            break
```

-   make_heap의 수행시간

    -   for문 k 호출을 n번 진행 X heapify_down수행시간
    -   n X heap의 height

-   heapify_down의 수행시간

    -   worst case => root노드부터 가장 깊은 레벨의 leaf node까지 heapify_down
    -   heap의 높이에 비례하게됨.
    -   따라서, heapify_down의 수행시간 -> **heap의 height**

-   heap의 height 계산

    -   root node -> 1
    -   root node의 자식 노드 -> 2
    -   자식의 자식의 자식의..... -> 2^2.....
    -   마지막 레벨의 노드는 2^(h-1)부터 2^h 중에 있음.
    -   1+2+2^2+....+2^(h-1)+1 <= n
    -   -> 2^h <= n
    -   -> h <= log(2)n

-   heapify_down : O(h) -> O(logn)
-   make_heap : O(nh) -> O(nlogn) -> **실질적으로 O(n)에 수렴** (sigma i=0 to h, 2^i\*(h-i)) -> O(n)
    -   make_heap 수행시간 -> sigma로 이루어진 수식을 멱급수 형태로 풀어주면 O(n)나옴

### insert와 delete_max 연산

-   insert
    1. A.append(14) (leaf노드로 추가)
    2. 부모 노드와 비교 -> 부모 노드보다 key값이 크면 위치 변경
    3. 부모노드의 동일한 레벨의 노드와 key값 비교할 필요 X (just 부모노드랑)
-   heapify_up
    -   A\[k\]를 root방향으로 이동하면서 heapify!

```text
# pseudo code
heapify(k):
    # A[k]를 heapify.
    while k>0 and A[(k-1)//2]<A[k]: # root node이거나 부모노드의 키값이 자식노드의 키값보다 크면 break
        A[k],A[(k-1)//2]=A[(k-1)//2],A[k]
        k = (k-1)//2
```

-   수행시간 - 트리의 높이 h = log(2)n 만큼 진행 -> O(logn)
-   A를 heap으로 만들기 위해서는 **A에 make_heap을 호출하거나 - O(n)시간**, **insert를 n번 호출한다. - O(nlogn)시간**

-   find_max

    -   return root node

-   delete_max - O(n)시간.
    1. root node를 삭제한다.
    2. 빈 root node를 채우는 방법!
    3. 가장 마지막 노드를 root node로 보낸다.
    4. root node를 heapify_down 한다.

```text
delete_max:
    if len(A)==0:
        return None
    key = A[0]
    A[0],A[len(A)-1] = A[len(A)-1],A[0]
    A.pop()
    heapify_down(index(0), len(A))
    return key
```

### Update_key 연산

-   old_key와 new_key가 들어있는 인덱스를 어떻게 찾는가?
-   애초에 데이터를 key와 index를 함께 저장
-   dictionary를 통해 D\[key\]를 입력 -> index가 나오도록 저장

```python
# pseudo code
def Update_key(self,old_key,new_key):
    if old_key>new_key:
        heapify_down(old_key)
    if old_key<new_key:
        heapify_up(old_key)
```

### 연산 정리

1. make_heap: O(n), O(nlogn) - insert n번 or heap 구축
2. insert : O(logn)
3. find_max : O(1)
4. delete_max : O(logn)
5. heapify_down : O(h) = O(logn)
6. heapify_up : O(h) = O(logn)

-   search연산은 하나하나 값을 비교하는 것 외에는 heap 자료구조만의 특별한 search 존재 X
-   heap은 search의 효율성 X -> **insert, find_max, delete_max**를 빠르게 진행하는 application에 적용!!!

-   **min_heap?**

    -   부모 노드와 자식 노드의 key값 관계를 반대로 정의하면 됨.
    -   부모 노드의 key값이 자식 노드의 key값보다 작거나 같도록 정의!
    -   root node가 최소값이 될 것. -> delete_min, find_min 파생

### heap_sort 알고리즘

```python
# pseudo code
def sort(A):
    n=len(A)
    for i in range(n-1, 0, -1):
        m, idx= get_max(A,i) # A[0]..A[i]까지 최대값 -> m에, 해당 인덱스는 m에 언패킹
        A[idx], A[i] = A[i], A[idx]
```

-   get_max에 heap 자료구조를 이용할 때 수행시간이 효율적으로 줄어들게 됨
