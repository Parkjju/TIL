# TRUE, FALSE 그리고 if와 그 형제들

### 참과 거짓을 의미하는 값(데이터)

```python
>>> 1>3 # 파이썬이 False를 반환하는 상황
False
>>> 1<3 # 파이썬이 True를 반환하는 상황
True
```

```python
# True False 반환값을 변수에 저장할 수도 있다.
>>> result  = 1<3
>>> print(result)
True
```

```python
>>> type(True)
<class 'bool'>
```

-   파이썬에게 True의 클래스를 물어보니 **bool** 이라고 대답하였다.

-   즉, 파이썬에서 True False 는 '부울형'이라고 불리우는 데이터임을 알 수 있다.

---

-   지금까지의 알게 된 파이썬에서의 데이터 종류

    -   int형 데이터 (1,2,3)
    -   float형 데이터 (2.2, 4.4)
    -   리스트형 데이터 ([1,2,3])
    -   스트링형 데이터 ("HI HI HI")
    -   부울형 데이터 (True, False)

---

### if문 : 조건이 맞으면 실행하라

-   if문의 기본 구조

    -   if<조건>:</br>
        <문장1></br>
        <문장2></br>

```python
if num>0:
    print("양수입니다") # if문도 마찬가지로 들여쓰기가 필수적.
```

```python
#위의 코드에 전달되었던 num값이 양수인 경우
if True:
    print("양수")
```

```python
#위의 코드에 전달되었던 num값이 음수인 경우
if False:
    print("양수?") # 들여쓰기로 if문을 구별
```

```python
# main함수를 만들어 프로그램 실행의 흐름 담기

def main():
    num=int(input("정수 입력:"))
    if num>0:
        print("양수")

main() #main 함수의 실행 명령
```

```python
# if문에 속하는 문장이 하나일 경우 다음과 같이 작성해도 무관

>>> num=2
>>> if num>0: print("양수")
```

### if~else문

-   if-else문의 기본 구조

-   if<조건>:</br> <참일 때 실행할 문장></br>else:</br> <거짓일 때 실행할 문장>

```python
def main():
    num = int(input("정수 입력: "))
    if num>0:
        print("양수")
    else:
        print("양수가 아닌 수")

main()
```

### if-elif-else문 : 여러 길 중에 하나만 선택

-   if<조건1>:</br> <조건 1 참일 시 실행></br>elif<조건 2>:</br> <조건 2 참일 시 실행></br>else:</br> <모든 조건 만족 못할 시 실행>

```python
def main():
    num = int(input("정수 입력:"))
    if num>0:
        print("양수")
    elif num<0:
        print("음수")
    else:
        print("0")

main()
```

### True 또는 False를 반환하는 연산들

-   <,>,<=,>=,==,!= -> 수(number)비교에 있어서 왼쪽에 놓인 수 기준으로 True, False값을 반환한다.

### if-else문의 중첩

```python
if num%2==0:
    if num%3==0:
        print("2의 배수이면서 3의 배수")
    else:
        print("2의 배수이지만 3의 배수는 아님")
else:
    print("2의 배수가 아님")
```

### and, or, not 연산자

```python
>>> True and True # 둘다 True일때 True반환
True
>>>
>>> True and False
False
>>>
>>> True or True # 하나만 True여도 True 반환
True
>>>
>>> True or False
True
>>>
>>> not False # True면 False, False면 True반환
True
```

-   and or not의 실질적 활용 예시

```python
>>>num=6
>>>(num%2)==0 and (num%3)==0 #num이 2의 배수이면서 3의 배수라면
>>>TRUE
```

### 리스트와 문자열을 대상으로도 동작하는 비교연산자 !

```python
>>> 'abc'=='abc' #두 문자열이 같은가?
True
>>> 'abc'!='abc' #두 문자열이 다른가?
False
```

```python
>>> [1,2,3]==[1,2] #두 리스트가 같은가?
False
```

### True 또는 False로 답하는 함수들

-   s.isdigit() -> 문자열s가 숫자로만 이루어져 있으면 True

-   s.isalpha() -> 문자열s가 알파벳으로만 이루어져 있으면 True

-   s.startswith(prefix) -> 문자열 s가 입력된 문자 prefix로 시작하면 True

-   s.endswith(suffix) -> 문자열 s가 입력된 문자 suffix로 끝나면 True

---

-   현재까지 배운 문자열 내용 일부를 확인하는 함수들

    -   s.find(sub) -> 문자열 앞에서부터 sub를 찾아 인덱스 값 반환

    -   s.rfind(sub) -> 문자열 뒤에서부터 sub를 찾아 인덱스 값 반환

    -   s.startswith(prefix)

    -   s.endswith(suffix)

-   만약 문자열 내에 특정 문자나 문자열 포함이 되어있는 지에 대해 인덱스 값이 아닌 **단순 포함 여부** 만에 관심이 있을 경우
    --> in, not in 함수를 이용한다

```python
>>> if "abc" in s:
        print("있삼")
    else:
        print("없삼")

```

```python
# 문자열 뿐만 아니라 리스트에도 in 함수 적용 가능
>>> if 3 in [1,2,3]:
        print("잇삼")
    else:
        print("없")
```

```python
# hello 문자열 내에 he라는 문자열이 없냐고 질문!
>>> if "he" not in "hello":
        print("X")

# he라는 문자열이 hello라는 문자열 내에 포함되어 있으므로 False를 반환
```

---

-   지금까지 배운 수학기호로 이루어진 비교 연산자를 제외하고 단어로 이루어진 연산자들

    -   and

    -   or

    -   not

    -   in

    -   not in

---

### 수(number)를 True와 False로 인식하는 방식

```python
# 파이썬에서는 조건문의 조건에 0이 아닌 수가 오면 True로, 0이 오면 False로 인식한다
>>> num=1
>>> if num:
        print("num은 1이 아니다")
```

-   **조건문의 조건에 문자열이나 리스트가 온다면?**

```python
>>> bool("string")
True
>>> bool("") # 빈 스트링이 올 때 False반환
False
>>>
>>> bool([1,2,3])
True
>>> bool([]) # 빈 리스트가 올 때 False 반환
False
```
