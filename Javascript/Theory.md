# Theory

### ECMA Script?

-   JS에 ECMAScript - Specification 명칭, 이에 대한 업데이트가 ECS5, ECS6 ...
    -   -> 설명문 같은 역할. (JS 이용에 대한 설명서)

### Vanilla JS

-   JS의 한 종류. Library가 없음 (날 것의 JS)
-   바닐라 JS 학습 이후 Library 및 framework 추가된 JS 학습

### JS 추가하기

-   JS파일은 head에 추가 X
    -   body 맨 마지막에 추가.

```html
<!DOCTYPE html>
<html>
    <head>
        <title>!!</title>
        <link rel="stylesheet" href="index.css" />
    </head>
    <body>
        <h1>!!!</h1>
        <script src="index.js">
            // 이곳에 JS코드를 직접 입력해도 되고, src를 통해 파일을 불러오기도 가능
        </script>
    </body>
</html>
```

-   index.js에 경고 메세지 추가하기

```js
alert("Hello world");
```

<img src="../Javascript/images/hello.png" width="40%" height="40%"/>

-   index.js에 경고 메세지를 console log로 출력하기

<img src="../Javascript/images/hello2.png" width="40%" height="40%"/>
