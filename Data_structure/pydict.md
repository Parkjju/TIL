# python dictionary - hash table

-   resize - 초기 size == 8 (빈 딕셔너리)

    -   전체 슬롯의 2/3이 채워지면 크기를 2배로 resize하여 이사감
    -   **amortized time analysis** - 연산 횟수에 대한 수행시간을 평균으로 계산하는 방식
    -   resize후에 이사갈 때의 수행시간도 상수시간만큼 진행됨
    -   set:insertion, remove, search 수행시간이 **평균적으로 O(1)**

-   hash function
    -   파이썬의 built-in hash function이 존재함.
    -   hash function의 리턴 값이 크기 때문에 size로 적당히 나눈다

```python
hash("apple")
```

-   **collision resolution**

```text
# pseudo code
i = hash(key) % size
perturb = hash(key) # python의 perturb변수를 통해 search의 randomness 부여

while H[i] is not empty: # H[i] is occupied slot
    if H[i].key == key:
        # found!!
    # i = (i+1) % size -> linear probing
    i = (5*i+1 + perturb) % size -> 중복없이 모든 슬롯을 방문할 수 있게됨 (size가 2^n일때)
    perturb = perturb>>5
```

-   버전마다, 인터프리터마다 실제 구현은 다를 수 있지만 틀은 비슷
