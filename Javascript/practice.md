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

### JS DOM Functions

-   CSS에서의 셀렉터를 JS에서도 선택할 수 있다.

```css
h1 {
    color: tomato;
}
```

```html
<body>
    <h1 id="title">HA</h1>
</body>
```

```js
const title = document.getElementBtId("title");
console.log(title);
//  <h1 id=title".... 출력됨
```

-   **DOM : Document Object Module** -> **html의 모든 요소를 가져와 객체로 바꿈.**
-   JS의 힘 -> 배울 모든 함수들, 찾게 될 모든 함수들을 DOM객체로 바꿀 수 있음.

### Modifying the DOM with JS

-   JS로 HTML을 조종할 수 있음
-   click의 감지, 스타일의 변경 등...

```js
const title = document.querySelector("#title"); //document의 title id 찾기
const title = document.quearyselector(".title"); // document의 title class 찾기
```

### Events and event handlers

-   window event

```js
function functionName() {
    console.log("resized!!");
}

window.addEventListener("resize", funtionName); // js에게 어떤 이벤트가 발생할 지 알려야함.
```

-   함수를 즉시 호출하지 않고, 지정한 **resize**행위가 발생했을 경우에 functionName 함수를 호출하라.
-   함수에 parameter가 있는 경우? -> 나중에 논의 !!

-   click 이벤트 추가.

```js
const title = document.querySelector("title");
function handleClick() {
    title.style.color = "red";
}
window.addEventListener("click", handleClick);
```

-   click 이후에 해당 상태로 계속 머무르게됨. -> 조건문을 통해 수정하기

### if, else, and, or

-   if - else

```js
if (condition) {
    block; //console.log ....etc
} else {
    block;
}
```

-   비교연산자 -> **===**

-   and

```js
if (20 > 5 && "park" === "jun") {
    console.log("yes");
} else {
    console.log("No");
}
```

-   or

```js
if ("park" === "jun" || "park" === "park") {
    console.log("yes");
} else {
    console.log("no");
}
```

### DOM - if-else Function practice

-   [javascript DOM event MDN](https://developer.mozilla.org/ko/docs/Web/Events)

*   online event

```js
function handleOffline() {
    console.log("offLine");
}

function handleOnline() {
    console.log("Online");
}

window.addEventListener("offline", handleOffline);
window.addEventListener("online", handleOnline);
```

-   와이파이 끄면 offline event로 인식되어 실제로 handleOffline 함수가 호출됨!!
