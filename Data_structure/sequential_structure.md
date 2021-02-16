# 선형 구조

### Array(배열), List(리스트)

-   데이터를 **연속적인 메모리 공간** 에 저장하고, 저장된 곳의 **주소(address, reference)** 를 통해 매우 빠른 시간에 접근할 수 있는 가장 많이 쓰이는 자료구조

    -   C에서의 배열 -> 배열의 시작 주소, 저장된 값의 종류(바이트 개수), 몇 번째에 저장되어 있는지 나타내는 인덱스(index) 세 정보만으로 값이 저장된 곳의 주소 계산 가능!

        -   C의 배열은 읽기/쓰기 연산만 제공하는 제한된 자료구조

    -   Python에서의 list A (또는 tuple A)

        -   C언어 배열의 셀에는 실제 값(데이터)이 저장된 형식이지만, **Python 리스트의 셀에는 데이터가 아닌 데이터가 저장된 곳의 주소(address 또는 reference)** 가 저장된다.

        -   각 셀에서 데이터를 가리키고 있는 형태이며, 새로운 객체 생성 후 그 객체에 대해 접근 시 가리키던 객체는 그대로 두고 새로운 객체를 가리키게 되는 것.

        -   **리스트는 동적 배열이다**

            -   C언어의 배열과의 또 다른 중요한 차이점은 list의 크기(셀의 개수)가 필요에 따라 자동으로 증가, 감소한다는 것.

            -   append 또는 insert연산을 위한 공간이 부족하면 더 큰 메모리를 할당받아 **새로운 리스트를 만들고** 이전 리스트의 값을 **모두 이동한다.**

            -   반대로 pop연산을 하면서 실제 저장된 값의 개수가 리스트 크기에 비해 충분히 작다면 **더 작은 크기의 리스트를 만들고** **모두 이동한다.**

            -   위와 같이 필요에 따라 크기가 변하는 배열을 **동적 배열(dynamic array)** 라 부른다. -> 파이썬 사용자는 배열의 크기를 전혀 신경쓰지 않아도 됨!

            -   동적배열인 list를 위해서는 python내부적으로 현재 list의 크기 (capacity)와 list에 저장된 실제 값의 개수(n)를 항상 알고 있어야함. -> 해당 추가 정보를 위한 메모리가 필요하므로 빈 리스트 A는 0바이트보다 클 수 밖에 없다

```python
>>>import sys
>>> A = []
>>> sys.getsizeof(A) # 빈 리스트가 0바이트보다 큰 이유
64
>>>A.append("Python")
>>>sys.getsizeof(A)
96
```

#### 수행 시간

1. 인덱싱 연산 -> 값을 읽음 + 값을 쓰기 (읽/쓰 O(1))

2. append -> 평균적으로 O(1)

3. pop -> 평균적으로 O(1)

4. pop(index_value) -> pop(0) 이 worst case로, O(len(A))시간

5. insert -> 최악의 경우가 insert(0, value), 즉 삽입하는 인덱스값이 0일때 이므로 O(len(A))

6. remove -> worst O(n)

7. index, count -> O(len(A))

### Stack : LIFO, Queue = FIFO, DQueue; Stack + Queue

-   Stack -> Last In First Out 규칙

-   Queue -> First In First Out 규칙

-   DQueue -> Stack과 Queue 모두 지원

#### Stack

-   데이터는 리스트에 저장(append, pop함수 이용)

-   push, pop, top, isEmpty, size(Len)함수 내장된 자료구조

-   클래스 Stack 선언

```python
class Stack:
    def __init__(self): #생성함수 -> python초급편 클래스 단원 참조
        self.items=[] #데이터 저장을 위한 리스트

    def push(self,val):
        self.items.append(val)

    def pop(self):
        try:
            self.items.pop()
        except IndexError: #예외처리
            print("Stack is Empty") # pop할 아이템 X

    def top(self):
        try:
            return self.items[-1]
        except IndexError:
            print("Stack is Empty")

    def __len__(self): #스페셜 메소드로써, 함수 호출을 len(Stack_list)로 할 수 있게 해줌
    # len에 관련한 정보는 리스트에서 이미 관리하고 있기 때문
        return len(self.items)

    def isEmpty(self):
        return len(self)==0 # True, False반환

```

-   스택 사용 예시1) 괄호맞추기

```python
from Stack_python import Stack #스택 정의 후 메소드 import

def parChecker(parSeq): # 괄호 맞추기 함수
    S = Stack()
    for p in parSeq:
        if p=="(":
            S.push(p)
        elif p==")":
            if S.isEmpty():
                return False
            else:
                S.pop()
        else:
            print("Not allowed Symbol")

    if S.isEmpty():
        return True
    else:
        return False

# 여는 괄호를 계속해서 스택에 저장
# 닫는 괄호를 만나면 스택에서 여는 괄호를 추출하여 짝을 맞춰 소멸시켜준다
# 모든 작업, 즉 괄호로 주어진 수식에 대해 전체 루프를 끝마치고 나왔을 때 스택에 괄호가 남아있다면 짝이 맞춰지지 않았으므로 False를 반환


def parChecker2(parSeq): # 중괄호, 대괄호 추가
    S = Stack()
    for p in parSeq:
        if p == "(" or p == "[" or p=="{":
            S.push(p)
        elif p==")":
            if S.top()!="(":
                return False
            else:
                if S.isEmpty():
                    return False
                S.pop()
        elif p=="]":
            if S.top()!="[":
                return False
            else:
                if S.isEmpty():
                    return False
                S.pop()
        elif p=="}":
            if S.top()!="{":
                return False
            else:
                if S.isEmpty():
                    return False
                S.pop()
        else:
            print("Not allowed symbol")



    if S.isEmpty():
        return True
    else:
        return False

# 위의 소괄호 맞추기 방식과 전체적으로 동일
# 스택에 계속해서 저장하다가 닫는 괄호를 만났을 경우
# 닫는 괄호가 소,중,대괄호였다면 스택의 가장 위쪽에 있는 괄호 또한 소,중,대괄호로 똑같은 종류여야만 한다.
```

-   스택 사용 예시 2) infix를 Prefix로 변환

    1. 한 자리수 피연산자를 만나면 Prefix 변환 리스트 공간에 둔다
    2. 두 자리수 피연산자를 만나는 것을 check -> loop변수를 통해 함수에 전달되는 문자열의 이전 원소 또한 숫자임을 if로 확인 -> exp[loop-1].isdigit()
    3. 소수점 피연산자 만나는 것을 check -> 소수점 확인 후 이전에 Prefix변환 공간에 전달되었던 피연산자 숫자를 소수점과 결합한 상태로 변환 + 2차원 리스트 접근 방식을 통해 **가장 최근 리스트의 원소 - 문자열** 의 **가장 마지막 글자인 소수점.** 의 형태를 지니고 있다면 숫자 추가한 상태로 변환하여 prefix변환 공간에 전달. ->> 코드 확인 요망!
    4. 변환된 Prefix수식을 계산 함수에 전달
    5. 숫자를 스택에 쌓고 피연산자를 만날때마다 두 개씩 pop하여 연산자에 맞게 float변환 후 계산, 다시 push
    6. 최종 push된 하나의 마지막 원소가 바로 계산된 값

```python
from Stack_python import Stack #스택 메소드 import

def InfixToPrefix(exp): # infix를 prefix로 변환
    opstack = Stack() # 연산자operator를 담을 공간
    outstack = [] # 변환된 수식을 담을 공간
    loop=0 # 실수에 대한 연산이므로, 소수점이나 두자리수 이상 되는 피연산자에 대하여 접근하기 위한 방법 고안
    exp = exp.replace(" ","") # 연산자와 피연산자 사이에 공백 존재 가능성 배제

    for tok in exp:
        if tok == "*" or tok =="/":
            if opstack.top()=="^":
                oustack.append(opstack.pop())
                opstack.push(tok)
            opstack.push(tok)
            loop+=1
        elif tok == "^":
            opstack.push(tok)
            loop+=1
        elif tok == "+" or tok =="-":
            if opstack.top() == "*" or opstack.top()=="/" or opstack.top()=="^":
                outstack.append(opstack.pop())
                opstack.push(tok)
                loop+=1
            else:
                opstack.push(tok)
                loop+=1
        elif tok == "(":
            opstack.push(tok)
            loop+=1
        elif tok == ")":
            while opstack.top()!="(":
                outstack.append(opstack.pop())
            opstack.pop()
            loop+=1
        else:
            if outstack==[]: # loop를 통해 이전 토큰이 숫자였다면 두자리수 이상임을 확
                outstack.append(tok)
                loop+=1
            else:
                if exp[loop-1].isdigit():
                    newstr = outstack[-1]+tok
                    outstack[-1]=newstr
                    loop+=1
                elif tok=="." or outstack[-1][-1] ==".":
                    newstr = outstack[-1]+tok
                    outstack[-1]=newstr
                    loop+=1
                else:
                    outstack.append(tok)
                    loop+=1



    while not opstack.isEmpty():
        outstack.append(opstack.pop())

    return outstack


def Calculator(exp): # if token in '*+/-':
    S = Stack()
    for tok in exp:
        if tok in "*/-+^":
            a=float(S.pop())
            b=float(S.pop())
            if tok=="-":
                S.push(b-a)
            elif tok=="+":
                S.push(b+a)
            elif tok=="*":
                S.push(b*a)
            elif tok == "^":
                S.push(b**a)
            else:
                S.push(b/a)
        else:
            S.push(tok)
    return S.top()


```
