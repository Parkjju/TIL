# 클래스와 객체

### 전역변수와 지역변수

-   함수 안에 선언되는 변수 <지역 변수>

-   함수 밖에 선언되는 변수 <전역 변수>

```python
>>> def func(n):
        print(n) # 지역변수는 해당 함수 내에서만 접근 가능

>>> print(n) # n이라는 변수가 따로 선언되어 있지 않은 상태에서 함수 내의 지역변수에 접근하고자 하는 의도를 지녔을 때의 에러
Traceback (most recent call last):
  File "<pyshell#6>", line 1, in <module>
    print(n)
NameError: name 'n' is not defined
```

-   **지역변수는 함수 내에서 만들어졌다가 함수를 벗어나면 사라지는 변수이다."**

```python
>>> cnt = 100 # 전역변수의 선언
>>> def func():
        print(cnt) #전역변수에 저장된 값을 출력
>>> func()
100
```

```python
>>> cnt = 100 # 전역변수의 선언
>>> def func():
        cnt = 0
        print(cnt) # cnt는 전역변수?
>>> func()
0
>>> print(cnt)
100
```

-   위의 결과를 통해 알 수 있듯이 함수 내에서 전역변수와 이름이 같은 변수를 새로 선언하고 값을 저장하면 이는 지역변수 취급을 받게 된다.

-   함수 내에서 전역 변수에 접근하기 위해서는?

```python
>>> cnt = 100
>>> def func():
        global cnt # 이 함수에서 접근하는 cnt변수는 전역변수임을 알림
        cnt=10
        print(cnt)

>>> func()
10
>>> print(cnt) # 전역변수의 값 또한 변경되었음을 알 수 있다.
10
```

### 클래스와 객체의 이해

```python
class AgeInfo: # 클래스 AgeInfo의 정의
    def up_age(self): #한살 더먹는 함수
        self.age+=1
    def get_age(self): #나이 반환함수
        return self.age

def main():
    fa = AgeInfo() # AgeInfo의 객체를 생성, 변수에 저장
    # 현재 fa객체에 up_age와 get_age함수가 저장되어 있는 상태
    # up_age와 get_age에서 이용하는 age변수가 객체에 없으므로
    fa.age = 39   # fa객체에 age변수를 생성
    fa.get_age() # fa에 저장된 객체의 함수 get_age()호출
    fa.up_age() # fa에 저장된 객체의 함수 up_age() 호출
```

-   객체 안에 있는 변수 age는 어떤 변수일까?

-   객체 안의 변수는 지역변수도, 전역변수도 아닌 **인스턴스 변수** 이다. 더불어 객체 안에 있는 함수는 **메소드** 라고 한다.

-   인스턴스 변수 객체 안에 존재하는 '변수'를 뜻하는 말

-   인스턴스 메소드 객체 안에 존재하는 '함수'를 뜻하는 말

-   위의 fa = AgeInfo()를 표현하는 데에 있어서

-   **AgeInfo()의 객체가 생성되어 변수 fa에 저장되었다.** 라고 표현해도 되지만,

-   **AgeInfo()의 인스턴스가 생성되어 변수 fa에 저장되었다.** 라고 표현해도 된다.

-   인스턴스 변수와 인스턴스 메소드 재 정립
    -   인스턴스 변수 인스턴스(객체)안에 존재하는 변수
    -   인스턴스 메소드 인스턴스(객체)안에 존재하는 메소드(함수)

### self?

-   앞의 AgeInfo 클래스로부터 인스턴스를 셋 (아빠, 엄마, 나) 생성해보자.

-   각 객체를 따로 표현했을 때 함수가 따로 논다고 생각하게 된다. 객체에 존재하는 up_age함수와 get_age함수는 완전히 동일한 기능을 하는데도 말이다!

-   위에서 정의한 AgeInfo함수를 다시 봐보자

```python
class AgeInfo: # 클래스 AgeInfo의 정의
    def up_age(self): #한살 더먹는 함수
        self.age+=1
    def get_age(self): #나이 반환함수
        return self.age
```

-   fa변수로부터 클래스의 인스턴스 할당 및 함수 호출까지의 과정을 살펴보자

1. fa = AgeInfo() 연산을 통해 AgeInfo 클래스의 인스턴스를 fa변수에 저장

2. fa.up_age() 변수 fa에 저장된 객체의 함수를 호출

3. up_age(fa) 객체 내의 함수의 매개변수로 fa를 전달

4. 연산!

-   self를 통해 인스턴스 자기 자신을 매개변수로 전달할 수 있게 된다.

### self 이외의 매개변수를 갖는 메소드들

-   클래스 내에 메소드 생성시 self 이외에도 매개변수를 전달할 수 있다.

```python
class AgeInfo():
    def set_age(self,age):
        self.age = age
# 인스턴스 변수 => self.age
# 일반 매개변수  => age
# 인스턴스 변수와 매개변수의 이름은 동일해도 상관없음
```

### 생성자

-   객체 생성 후에 반드시 해줘야 하는 일이 하나 있다. ==> **인스턴스 변수의 초기화**

```python
def main():
    fa = AgeInfo()
    fa.age=20
```

-   위와 같이 객체를 생성한 뒤에는 객체의 인스턴수 변수들을 모두 초기화해야한다.

-   또한 이러한 초기화는 객체 생성 후 바로 하는 것이 일반적임.

-   파이썬은 객체의 생성과 변수의 초기화를 동시에 진행할 수 있도록 **생성자**를 제공

```python
class Const:
    def __init__(self):
        print("new") # __init__메소드

def main():
    o1 = Const()
```

```python
class Const:
    def __init__(self,var1,var2):
        self.var1=var1
        self.var2=var2 # Const클래스의 생성자 호출과 동시에 변수 초기화
    def show_dat(self):
        print(self.var1,self.var2)

def main():
    o1 = Const(1,2)
    o2 = Const(3,4)
    o1.show_dat(o1)
    o2.show_dat(o2)

main()
```

-   객체 생성시 생성자 메소드 **init**을 적극 이용하자

### 파이썬의 모든 데이터는(값은) 객체

```python
>>> s = "coffee"
>>> s.upeer()
'COFFEE' # upper함수의 호출이 가능하다는 것을 통해 문자열 데이터 s도 객체임을 파악
>>> n = 1000
>>> n.bit_length() # 변수 n에 담긴 정수도 객체
10
>>> f = 3.14
>>> f.is_integer() # 변수 f에 담긴 실수도 객체
False
```
