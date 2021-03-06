# 분할정복방법 (Divide & Conquer)

- 큰 문제를 작은 문제로 분할하여 재귀적으로 해결

```python
def max(A):
    return max(A[0], max(A[1:])) # .....
```

- T(n) = T(n-1)+c, T(1) = c, T(n) = O(n)

- 분할의 방법은 다양하다. 위처럼 하나씩 분할하여 선형적으로 재귀를 구현하거나, 반씩 나누거나.. `max(A[:4], max(A[4:]))`

  - T(n) = 2\*T(n/2) + c, T(1) = c, T(n) = O(n)

- 제곱수 계산 -> power(a,n) (a^n) = a\*a^(n-1)

  - 바닥조건 n==1 -> return a
  - else -> return a\*power(a,n-1)
  - T(n) = T(n-1) + c, T(1) = c, T(n) = O(n)

- 반씩 나누어서 설계

  - `if n==1: return a`, `if n==0: return 1`
  - `a^n = a^(n/2) * a^(n/2)` -> n (n에 대해 짝 홀수 구분)
  - 1. 짝수 -> `return power(a,n//2) * power(a, n//2)`
  - 2. 홀수 -> `return power(a,n//2) * power(a, n//2) * a`

- 비선형적으로 설계
  - `if n==0: return 1`
  - `x = power(a, n//2) # x = a^(n/2)`
  - `if n%2 == 0: return x*x`
  - `else: return x * x * a`
  - 재귀적 호출이 한번에서 끝남 -> T(n) = T(n/2) + c, T(1) = c
  - T(n) = T(n/4) + c + c.... = T(n/(2^k)) + kc = k(c+1) = O(logn), T(n/(2^k))가 T(1)이 될때까지 -> k=log2(n)
  - T(n) = T(1) + kc = c + kc = c(k+1)
