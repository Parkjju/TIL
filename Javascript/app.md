# MAKE YOUR FIRST JS APP

### Making a JS Clock

-   Date 객체 이용

```js
function getTime() {
    const date = new Date();
    const minutes = date.getMinutes;
    const hours = date.getHours;
    const seconds = date.getSeconds;
}
```

-   새로고침을 해야만 시간이 update되는 문제가발생. -> **setInterval**함수를 이용!!

-   argument 두개 -> (function, 실행할 시간 간격)
-   **milliseconds**단위 !!

```js
function sayHi() {
    console.log("hi");
}

setInterval(sayHi, 3000);
```

-   js 삼항연산자 - 시간 표시에 00:00:00 형태로 나오지 않는 경우
-   if_condition ? True_value : False_value

```js
function getTime() {
    const date = new Date();
    const minutes = date.getMinutes;
    const hours = date.getHours;
    const seconds = date.getSeconds;
    clockTitle.innerText = `${hours}:${minutes}:${
        seconds < 10 ? `0${seconds}` : seconds
    }`;
}
```

### saving the user name

-   **local storage?**
-   브라우저에 데이터가 저장됨. (새로고침 해도 남아있다)

```js
localStorage.setItem("nico", true);
// nico에 true라는 데이터가 저장
localStorage.getItem("nico");
//nico라는 key를 찾아봄 -> true를 반환
localStorage.getItem("Park");
//park이라는 key 찾아보지만, 저장되어있지 않기 때문에 null반환
```

-   form에 데이터 입력후 Enter하면 default동작에 의해 소멸되게 됨. 이를 방지하기 위해 **preventDefault**메소드 이용

```js
function handleSubmit(event) {
    event.preventDefault();
}
```

-   해당 함수 정의 이후에 enter입력하여도 아무 일도 일어나지 않게됨.
-   input태그 셀렉트 -> value메소드 이용
-   이후 paintGreeting 함수 호출

```js
function handleSubmit(event) {
    event.preventDefault();
    const currentValue = input.value;
    paintGreeting(currentValue);
}
```

### Making a To Do List

-   데이터 입력 시 버튼 및 리스트가 생성 -> **createElement** 메소드이용

```js
const delBtn = document.createElement("button");
const li = document.createElement("li");
```

-   span 생성 -> span안에 todo 텍스트 삽입.
-   이후 li의 child로 span과 삭제 버튼을 삽입
-   child 추가 -> **appendChild메소드 이용**
-   마지막에 toDoList변수에 child 추가

```js
span.innerText = text; //text : 함수 argument, todo.js참조
li.appendChild(delBtn);
li.appendChild(span);
```

-   todo 리스트에 목록 추가하기
    1. toDos 배열에 리스트를 추가하는 방식 -> 추가할 때마다 해당 배열의 길이를 id로 이용
    2. 해당 아이디를 리스트에도 부여한다 (이후 버튼 클릭으로 삭제를 구현하기 위함)
    3. 리스트를 localstorage?
-   브라우저는 JS 데이터를 저장할 수 없다. (local storage 모든 데이터를 string으로 저장하려고 함.) -> object 저장하기 불가 -> **JSON.stringify**를 이용. **->JS obj를 string으로 바꾸어줌**

```js
function saveToDos() {
    localStorage.setItem(TODOS_LS, JSON.stringify(toDos));
}
```

-   **JSON이란?** - JavaScript Object Notation의 준말 - 데이터를 전달할 때 JS가 그걸 다룰 수 있도록 object로 바꾸어주는 기능

-   toDos 불러오기

    -   JSON의 parse 메소드 이용. (string으로 불러온 todo목록을 object로 다시 변환)

-   JS array의 forEach메소드 - **array 각 원소에 한번씩 함수를 실행시켜줌**
    -   foreach 내에서 만들거나, 외부 함수 이름을 넣으면 됨

```js
parsedToDos.forEach(function (toDo) {
    console.log(toDo.text);
});
//or
parseToDos.forEach(function_name);
```

### todo 삭제기능

-   event argument에는 **.target기능이 존재**
    -   event.target은 이벤트 버블링의 가장 마지막에 위치한 최하위 요소를 반환 (클릭된 요소의 최하위..)
-   Node.removeChild()

### background images

-   이미지에 순서가 있도록 숫자로 이름을 부여.
-   이후 js math모듈 이용하여 난수 (이미지 숫자 범위에 따라) 생성하여 랜덤하게 todo list 배경이미지 변화주기
-   Math.random()메소드를 이용
-   Math.ceil() 올림. Math.floor() 버림

```js
function paintImage(imgNumber) {
    const image = new Image();
    image.src = `images/${imgNumber + 1}.jpg`;
    body.appendChild(image);
}
function genRandom() {
    const number = Math.floor(Math.random() * IMG_NUMBER);
    return number;
}
```
