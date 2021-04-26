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

### Getting the Weather part one geolocation

-   navigator모듈 이용
    -   navigator.geolocation.getCurrentPosition(arg1, arg2)
    -   arg1 - 좌표정보 얻어내는데 성공하였을 때 다루는 함수
    -   arg2 - 좌표정보 얻어내는데 실패하였을 때 다루는 함수

```js
function handleGeoSuccess(position) {
    console.log(position);
}

function handleGeoError() {
    console.log(`Cant access geo location`);
}

function askForCoords() {
    navigator.geolocation.getCurrentPosition(handleGeoSuccess, handleGeoError);
}

function loadCoords() {
    const loadedCoords = localStorage.getItem(COORDS);
    if (loadedCoords === null) {
        askForCoords();
    } else {
        //getweather
    }
}
```

1. storage에 좌표 정보가 null
2. 좌표 요청 - getCurrentPosition 메소드
3. 요청 성공시 position 객체를 success함수로 자동 전달하여 출력하게 됨 (여러가지 정보가 포함)

-   정상 작동시 출력되는 객체

```js
GeolocationPosition {coords: GeolocationCoordinates, timestamp: 1619444366778}
coords: GeolocationCoordinates
accuracy: 1225
altitude: null
altitudeAccuracy: null
heading: null
latitude: 37.2801536
longitude: 127.1627776
speed: null
__proto__: GeolocationCoordinates
timestamp: 1619444366778
__proto__: GeolocationPosition
```

### weather API 다루기

-   [weather API site](https://openweathermap.org/)
-   가입 후 계정 - My API keys - API key 복사하여 js파일 변수에 할당

-   **API란?** - 특정 웹사이트로부터 데이터를 얻거나 컴퓨터(machines)끼리 소통하기 위해 고안된 것.

-   By geigraphic coordinates - API call실습
-   JS를 통해 특정 URL호출하는 법
    -   JS는 웹사이트로 request를 보내고 응답을 통해 데이터를 얻을 수 있음
    -   가져온 데이터를 refresh없이도 나의 웹사이트에 적용시킬 수 있음
-   fetch(`https:// ~~~~`); - 백틱 안에 https:// + API call 코드

-   chrome - inspect - network패널 -> 우리가 request한 내용을 보여줌
    -   network 패널의 response - 응답받은 데이터를 볼 수 있음

*   URL에 &units=metric 덧붙여서 섭씨온도로 바꾸기

```js
{"coord":{"lon":127.1628,"lat":37.2802},"weather":[{"id":802,"main":"Clouds","description":"scattered clouds","icon":"03n"}],"base":"stations","main":{"temp":13.62,"feels_like":12.89,"temp_min":13,"temp_max":15,"pressure":1020,"humidity":71},"visibility":10000,"wind":{"speed":0.51,"deg":150},"clouds":{"all":40},"dt":1619446486,"sys":{"type":1,"id":5509,"country":"KR","sunrise":1619383359,"sunset":1619432125},"timezone":32400,"id":6573747,"name":"Dongjinwon","cod":200}
```

-   210426기준 날씨정보

*   then=>온점(.)이전 작업이 완전히 끝난 후 괄호 안의 내용을 실행시킴.

*   이렇게 하지 않고 평소처럼 ;로 문장을 끝나고 바로 다음 문장을 썼을 경우,

*   이전 작업이 시간이 걸려 다 완료되지 않았는데도 다음 문장이 실행되어 오류가 발생할 수 있음.
