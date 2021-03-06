# 스택을 이용하여 계산기 코드 구현하기

### 각 토큰이 갖는 의미 구분하기

-   이항연산자 (binary operator)

    -   2+3, 3\*5 -> 피연산자 두개가 필요한 연산자

-   단항연산자 (unary operator)
    -   +3, -6

### infix to postfix

-   2+3*5 -> 2 3 5 * +

1. 괄호 치기 -> (2+(3\*5))
2. 연산자의 오른쪽 괄호 다음으로 연산자 이동. -> (2+(35)\*) -> (2(35)\*)+ -> 235\*+
3. 괄호 지우기 -> 235\*+

-   괄호가 이미 있는 경우. - 3*(2+5)*4 - infix to postfix
-   ((3*(2+5))*4) -> (3\*(25)+\*4) -> (325+\*\*4) -> 325+\*4\*

### 수식 변환

-   입력 - +, -, \*, (,), 숫자(영문자)로 구성된 infix수식
-   출력 - postfix

-   각 연산자의 우선순위 파악 (스택에 쌓을지 말지 결정하는 기준)

    1. 왼쪽괄호 ( -> 우선순위 가장 낮음
    2. +, - 우선순위 2번째로 낮음
    3. \*, / 우선순위 +,-보다 높음
    4. ) 오른쪽괄호가 가장 우선순위 높음

-   -> 오른쪽괄호 만나면 전체 연산자 빼면서 연산 시작

# 스택을 이용한 계산기 구현 완성 (클린하게 수정 필요)

1. get_token_list(expr)

    - expr - 수식을 문자열로 입력받아 전달
    - expr을 연산자와 피연산자로 나누어 리스트에 담은 후 리턴
    - -, +, \*, /, ^ 다섯개의 이항 연산자만 고려
    - 한 자리 이상의 실수 등장 가능.

2. infix*to* postfix(token_list):

    - get_token_list에서 리턴된 토큰리스트를 전달
    - 이를 postfix순서로 바꿈

3. compute_postfix(token_list)
    - postfix 순서의 token_list 수식 계산하여 리턴
    - 계산하기 전 피연산자를 float로 변환한 뒤 계산해야함.

```python
class Stack:
    def __init__(self):
        self.items = []

    def push(self, val):
        self.items.append(val)

    def pop(self):
        try:
            return self.items.pop()
        except IndexError:
            print("Stack is empty")

    def top(self):
        try:
            return self.items[-1]
        except IndexError:
            print("Stack is empty")

    def __len__(self):
        return len(self.items)

    def isEmpty(self):
        return self.__len__() == 0


def get_token_list(expr):
	result_token_list = []
	nonblank_token_list = expr.split()
	is_first = 0
	is_minus=0
	for i in nonblank_token_list:
			if i.isdigit():
					result_token_list.append(i)
			else:
					token = ''
					for j in i:
							if (nonblank_token_list[0][0] == '-' or nonblank_token_list[0][0] == '+') and j==nonblank_token_list[0][0] and is_first==0:
									token += j
									is_first+=1
							elif j in "+-*/^()":
									if result_token_list != [] and result_token_list[len(result_token_list)-1] == '(' and is_minus==0 and token=='':
											token+=j
											is_minus+=1
											continue
									if token != '':
											result_token_list.append(token)
									result_token_list.append(j)
									token = ''
							else:
									token += j
					if token != '':
							result_token_list.append(token)
	return result_token_list


def infix_to_postfix(token_list):
	opstack = Stack()
	outstack = []

	prec = {}
	prec['('] = 0
	prec['+'] = 1
	prec['-'] = 1
	prec['*'] = 2
	prec['/'] = 2
	prec['^'] = 3

	for token in token_list:
			if token == '(':
					opstack.push(token)
			elif token == ')':
					while opstack.top() != '(':
							outstack.append(opstack.pop())
					opstack.pop()
			elif token in '+-/*^':
					if opstack.isEmpty():
							opstack.push(token)
							continue

					while not opstack.isEmpty():
							if prec[token] > prec[opstack.top()]:
									opstack.push(token)
									break
							else:
									outstack.append(opstack.pop())

					if opstack.isEmpty():
							opstack.push(token)
			else:
					outstack.append(token)

	while not opstack.isEmpty():
			outstack.append(opstack.pop())

	return outstack


def compute_postfix(token_list):
	calstack = Stack()
	for token in token_list:
			if token in '+-/*^':
					first = float(calstack.pop())
					second = float(calstack.pop())
					if token=='^':
							calstack.push(second**first)
							continue
					result = str(second) + token + str(first)
					calstack.push(eval(result))
			else:
				calstack.push(token)
	return calstack.top()


# 아래 세 줄은 수정하지 말 것!
expr = input()
value = compute_postfix(infix_to_postfix(get_token_list(expr)))
print(value)
```

### 구현 시 고려했던 테스트케이스

1. -3\*2
    - 맨 앞의 마이너스 부호를 일반 연산자로 생각하면 이를 토큰으로 취급하여 이후 compute에서 스택에 오류가 발생한다
    - -3을 한 토큰으로 취급할 수 있도록 구현해야함.
2. -3\*(-2)
    - 이 또한 위의 테스트케이스와 마찬가지임.
    - 여는 괄호 뒤의 - 부호가 -2로 합쳐져서 토큰으로 전달될 수 있게 구현해야됨
3. 지수 구현의 경우 삽질함. 지수를 굳이 마이너스 플러스로 생각할 필요가 없음. 파이썬 내장 수식함수 \*\*를 사용
4. 빈칸에 대해서 모두 split된 형태로 반복문을 중첩시켰지만 별로 좋은 구조로 보이지 않음. - 심플하게 바뀌어야할듯
