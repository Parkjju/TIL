# CSS ADVANCED

### Transitions

-   CSS state를 통해 선택한 요소가 특별한 상태일 때 만족되는 상황들을 만들 수 있다.

-   예) :hover를 적용하면, 포인터를 해당 요소에 올려놓아야 상태의 변화가 일어난다.

```html
<style>
    button:hover {
        color: blue;
    }
</style>
```

-   상당히 cool하지 못한 모습이기 때문에 transition프로퍼티를 이용하여 이를 자연스럽게 꾸며준다

-   state선언 되어있는 곳이 아닌 외부 공간에 스타일을 따로 지정해야 한다.

```html
<style>
    a {
        color: tomato;
        background-color: wheat;
        transition: color 1s ease-in-out;
    }
    a:hover {
        color: red;
        background-color: black;
    }
</style>
```

-   위를 보면, hover 상태 만족 시 스타일 안에 transition을 넣은 것이 아니라 외부 a 태그 지정에 transition 프로퍼티를 넣었음을 관찰

-   transition이 state 지정되어있는 프로퍼티들을 찾아 전환 스타일에 대한 설정을해줌.

-   state설정해준 모든 프로퍼티에 대해 transition설정을 하고싶다면 all을 이용!

```html
<style>
    a{
        color:tomato;
        background-color:black;
        transition:all 1s ease-out;
    }
    a:hover{
        color:red;
        background-color:white;
    }
```

### transition part two

-   transition 프로퍼티에는 ease-in function이라는 것이 존재한다.

-   브라우저에게 애니메이션이 어떻게 변할 지에 대해 알리는 함수이다

```html
<style>
    a {
        color: tomato;
        transition: all 1s ease-in-out;
    }
</style>
```

-   위 코드에서 ease-in-out에 해당하는 부분.

-   ease-in-out 등등 여러 옵션들이 있지만, cubic-beizer라는 옵션을 통해 더 디테일한 애니메이션으로 꾸밀 수 있다.

```html
<style>
    a {
        color: wheat;
        background-color: tomato;
        text-decoration: none;
        padding: 3px 5px;
        border-radius: 5px;
        font-size: 55px;
        transition: color 1s cubic-bezier(0.6, 0, 0.735, 0.045), border-radius
                5s ease-in-out;
    }
    a:hover {
        border-radius: 20px;
        color: tomato;
        background-color: wheat;
    }
</style>
```

-   여러 옵션들을 한번에 transition 적용시키고 싶으면 쉼표를 통해 구분하면 됨! (위의 코드 참고)

### Transformation

-   transform 프로퍼티 - 이미지 등에 대해 전환

-   scaleX, scaleY, matrix, rotateX,Y,Z ... 너무나 많은 옵션들이 존재함.

-   [Transform 프로퍼티 옵션 참고](https://developer.mozilla.org/ko/docs/Web/CSS/transform)

-   Transform 프로퍼티는 transition 프로퍼티와 함께 쓰일 때 진정 cool한 모습을 보인다

```html
<style>
    img {
        border: 10px solid black;
        border-radius: 50%;
        transition: all 2s ease-in-out;
    }
    img:hover {
        transform: rotateX(50deg);
    }
</style>
```

-   각도에 대한 단위 -> deg

-   rotate 옵션에 대해 자연스러운 움직임을 부여하기 위해 root 태그에 transition 프로퍼티를 **무조건** 부여하자!

-   기본 transform 옵션들

    1. scale - X, Y기준 늘이기 (Z축은 안됨)

    2. rotate - 회전

    3. translate - 이동

-   CSS로 3D 애니메이션 구현 가능하게 된 것은 브라우저의 진보 + 컴퓨터 GPU의 활용으로 인함!

-   **transform프로퍼티는 다른 요소의 box에 영향을 주지 않는다.** 페이지의 픽셀 차원에서 일어나는 변화이고 box 자체에 대한 변화가 일어나지 않음.

-   따라서 형제 요소가 인식하기를, transform이 일어난 요소에 대해서 그 요소가 제자리에 있는 것으로 인식함.
