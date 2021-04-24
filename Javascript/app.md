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
