# PRACTICE

```js
console.log(console);
```

-   console 안에 포함되어 있는 여러 함수들 목록의 출력..
-   객체로서의 console

### 함수의 정의

-   argument도 안받고, return값도 없음

```js
function sayHello() {
    console.log("Hello!");
}

sayHello();
```

-   argument (parameter)가 있는 상황

```js
function sayHello(potato) {
    console.log("Hello!", potato);
}
```

-   console.log 함수에 string 연결하기 (백틱 `이용)

```js
// 기존방식
console.log("Hi" + "HAHA");
// 현재 사용방식 - 백틱 이용 string (함수 이용, parameter필요)
function sayHello(name, age) {
    console.log(`Hello ${name} you are ${age} years old`);
}
```

-   함수에 return 적용

```js
function sayHello(name, age) {
    return console.log(`Hello ${name}, ${age}`);
}
const greet = sayHello("Park", 10);
```

-   **객체 안에 함수 구현하기**

```js
const calculator = {
    plus: function (a, b) {
        return a + b;
    },
};

const plus = calculator.plus(5, 5);
console.log(plus);
```
