# 해시 테이블 (Hash Table)

-   해시 테이블은 일종의 사전(dictionary)이고, Python의 dict 자료구조처럼 insert, remove, search 연산을 빠르게 지원한다
-   (데이터 item이 key&value쌍으로 구성된다고 가정)

    1. insert(key,value) -> (key, value)를 해시 테이블에 저장, 같은 key가 있으면 overwrite
    2. remove(key) -> (key,value)가 해시 테이블에 있으면 삭제
    3. search(key) -> (key,value)찾아서 리턴

-   사용 분야 - database, compilers&interpreters, document similarity, network router, substring search, file/directory synchronization, **cryptography** .... 매우 중요

-   **예시**

1. key값이 학번이고, value가 이름인 item이 있다고 가정
2. key를 10으로 나눈 나머지를 인덱스로 하는 장소에 value를 저장한다.
3. 201701342를 10으로 나눈 나머지 -> 인덱스 2에 value를 저장.
4. 이후 원하는 연산 진행 시 key 탐색에 있어서 **key를 10으로 나눈 나머지에 대한 연산만 진행하면 된다**

-   위의 예시에서 볼 수 있듯, key값을 key값이 저장될 index로의 mapping을 진행해주는 function을 **해시 함수(hash function)이라고 한다.**

-   **collision**?

-   구현되어 있는 hash function을 통해 특정 index에 접근을 시도하는데, 이미 다른 item이 저장되어 있었다면 이를 충돌(collision)이 발생했다고 한다.

-   이를 해결하는 방법을 **충돌해결방법(collision resolution method)라고한다.**

### 위의 내용까지 정리

1. Table은 기본적으로 List로 구현된다.
2. Hash function에 대한 결정
3. Collision resolution method 구현에 대하여

-   해시 테이블은 2,3번이 잘 구현되어 있는지 여부에 따라 전체적인 성능이 결정된다.

### 해시 함수(hash function)

-   좋은 hash function?
    1. less collision
    2. fast computation
-   이 둘은 어느 정도 trade-off한 부분이 있기 때문에 적절히 두 비율을 조정해야함

1. perfect hash function : key -> slot에 1대1로 대응 되는 것. **(ideal hash function) -> 비현실적**
2. universal hash function?
    - 각각 x, y key값을 가지는 item이 있다고 가정. Prob(f(x)==f(y))은 collision이 발생할 확률이며 슬롯의 개수를 m이라고 가정하면 universal hash function은 **Prob(f(x)==f(y))= 1/m** 을 만족해야한다.
    - 확률을 1/m 으로 설계하는 것도 어려움
3. c-universal hash function : universal hash function의 collision확률이 **c/m**인 hash function

### 현실에서 자주 쓰이는 해시 함수들

1. Division : f(k) = (k mod p) mod m (p는 소수)

2. Multiplication : f(k) = (ak) mod 2^w) >> (w-r)

    - a:랜덤 값, w = log(r), r = log(m)

3. Folding : key값의 digit을 나눠 연산하는 형식

    1. shift folding 예시 ) 계좌번호 - 1234-567-890을 두 digit씩 나누어 모두 더한 후 mod m. (12+34+56+78+90) mod m
    2. boundary folding : 여러 digit으로 나눈 후 더하는 데, 짝수번 조각은 거꾸로 해서 더함
        - 12+**43**+56+**87**+90 mod m

4. Mid-Square : key값을 적당히 연산 후 그 결과의 중간 부분을 떼어내 주소로 이용

    - m=1000이라고 가정, key=3121일 때 key^2 = 97**406**41의 중간 digit 406을 주소로 이용

5. Extraction : key 값의 각 파트마다 임의의 digit을 떼어내 연결하여 계산
    - 계좌번호가 1234-567-890이면, 1234에서 12, 567에서 7을 떼어내 **127**을 주소로 만듦.

### 현실에서 자주 쓰이는 해시 함수들 - key값이 문자열일 때

1. Additive hash : key[i]의 단순 합 - ASCII값
2. Rotating hash : <<,>> 비트쉬프트 연산과 ^(exclusive or)연산을 적당히 반복
3. Universal hash
    - Bernstein hash
    - C++ STLPort 4.6.2 hash
    - java.lang.String.hashCode()

<!-- Todo: hash function들 실습해보기 -->
