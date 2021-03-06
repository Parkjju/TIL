# CSS 기초

### HTML에 CSS 추가하는 방법

1. 같은 HTML파일에 CSS & HTML코드를 배치 => head내에 style태그를 이용한다.

2. CSS와 HTML분리하기 -> 권장되는 방법 (style.css생성 후 link태그의 href속성을 통해 접근 + rel="stylesheet"지정)

rel = relationsip의 약자로, 링크된 파일과의 관계를 설명

3. link:css -> 외부 css파일 참조 뼈대코드 자동생성됨

### CSS 코드 작성법, 3가지 규칙

1. 셀렉터(selector)가 HTML 태그를 가리킨다.

2. 프로퍼티(property)가 HTML태그의 속성을 지정한다.

3. CSS => Cascading style sheet임을 기억하자.

(파일을 통해 external CSS를 지정하고, 파일 내부에서 inline CSS를 지정했지만

만약 같은 태그에 대해 이루어진 것이라면?

(**cascading 성질로 인해 아래에 위치한 코드로 결국 적용된다.**)

-   예시)

```css
<style>
    h1{
        color:blue;
    }
</style>
```

-   **프로퍼티 이름은 띄어쓰기가 불가능**하며, 속성 지정시 **콜론(:)**, 속성 지정 후에는 **세미콜론(;)** 표기로 항상 마무리지어야한다.

### Blocks and inlines

-   Blocks의 성질을 지닌 태그들은 옆에 또 다른 block이 오지 못한다.</br>(div, header, main, section 등등)

-   Block과 반대로 inline성질을 지닌 태그들은 옆에 다른 요소가 올 수 있다.

### Margin

-   block을 inline으로 바꾸기 또는 반대의 경우를 진행 -> display프로퍼티 만지기

```css
.box {
    display: inline;
}

.nonbox {
    display: block;
}
```

-   (참고)inline요소는 너비와 높이를 가지지 않기 때문에, **태그 내에 컨텐츠의 크기만큼만 공간을 차지**하며 컨텐츠가 없으면 출력되는 것이 없다.

```html
<!DOCTYPE html>
<head>
    <style>
        header {
            display: inline;
            height: 100px;
            width: 100px;
            background-color: tomato;
        }
    </style>
</head>
<body>
    <header></header>
    <header></header>
</body>
```

-   (참고) CSS설정시 특정 프로퍼티에 대해 값을 할당하지 않은 채 html파일을 생성하면</br>브라우저의 종류에 따라 기본 설정값을 할당받아 생성되게 된다.</br> 그 중 하나로 margin값이 있다</br>

-   margin 프로퍼티에 값을 몇개 할당하느냐에 따라 적용되는 방향이 달라진다.

```css
header{
    margin:10px; <!-- box 상 하 좌 우 적용-->
}

header{
    margin:10px 15px; <!-- 상하 & 좌우-->
}

header{
    margin: 10px 15px 20px; <!-- 첫번째는 상, 두번째는 좌우, 세번째는 하-->
}

header{
    margin: 10px 15px 20px 25px; <!-- 상우하좌, 시계방향-->
}
```

### 여백상쇄란?(Collapsing Margin)

> 여러 블록의 위쪽 및 아래쪽 바깥 여백(마진)은 경우에 따라 제일 큰 여백의 크기를 가진 단일 여백으로 결합(상쇄)되곤 합니다. 이런 동작을 여백 상쇄라고 부릅니다. 단, 플로팅 요소와 절대 위치를 지정한 요소의 여백은 절대 상쇄되지 않습니다. - MDN

-   쉽게 말해, Block요소가 상 하로 존재하며 상하좌우 height,width 값을 모두 20px로 주었을 때</br>
    <img src=images/margin.PNG width="100%" height="100%"></img>

*   위의 이미지와 같이 윗 블록 요소의 하단부, 아래 블록 요소의 상단부가 겹쳐 </br>본래 200px 가 되어야 할 마진 너비가 100px로 상쇄되어 버린 것이 바로 margin collapsing 현상이다.

*   이는 부모-자식 Block요소에서도 발생한다.

```css
.parent {
    margin: 0;
}

.chi {
    margin: 50px;
}
```

-   위와 같은 클래스로 지정된 부모-자식 블록 태그가 있다고 가정하자.

<img src="images/margin2.jpg" width="100%" height="100%"></img>

-   허접하지만 위의 그림을 설명해보자면, 분명 부모 블록 요소의 클래스의 margin값을 0으로 지정했음에도 자식 블록 요소의 margin값이 50px였기 때문에 부모 블록 요소의 상단부에 여백이 생기게 된다.

-   이 경우는 개발자 입장에서 원하지 않는 형태의 구현이 될 수 있기 때문에 </br>해당되는 케이스의 여백상쇄 현상을 일어나게 하지 않기 위해서는 공간을 차지하는 컨텐츠를 넣어줘야된다. </br>하지만 쓸모 없는 텍스트를 집어넣을 수는 없으니 부모 블록 요소에 padding값을 지정함으로써 이를 방지한다.

### paddings and IDs

-   padding opposite margin -> padding은 box의 안쪽공간을 지정한다.

-   같은 요소에 차이를 두는 법 => id attribute 지정 후 </br>
    style태그 내에서 #(해시태그)이용하여 프로퍼티 지정 (#id_name)

```css
#exciting {
    background: linear-gradient(to bottom, #ffe8d4, #f69d3c);
    border: 1px solid #696969;
    padding: 10px;
    border-radius: 10px;
    box-shadow: 2px 2px 1px black;
}
```

### border

-   border : size style color;

### classes

-   inline 요소는 너비와 높이의 개념이 없고, margin또한 좌-우만 적용 가능하다.

-   padding의 경우는 상하좌우 모두 적용 가능하다.

-   CSS class -> 같은 태그 특정 컨텐츠에 다른 프로퍼티를 적용하고 싶을 때 이용한다.

-   ID의 경우 unique해야한다는 속성으로 인해 효율이 떨어진다.

```css
#ID_one,
#ID_two,
#ID_three {
    color: tomato;
}
```

-   ID로 여러 태그들 지정 시 위와 같이 한 번에 묶을 수 있다.

-   ID를 이용할 때 가장 큰 문제는, 특정 요소에 대하여 속성을 지정하고싶은데, 한 요소의 color를 red, 다른 요소의 color를 black 으로 설정하고 나머지의 프로퍼티를 동일하게하고싶을 때 비슷한 코드를 여러 번 작성해야하는 점이 비효율적이다.

-   id선택자는 요소당 하나밖에 지정 불가 !

-   class 지정 기본 구조는 다음과 같다

```html
<style>
    .class_name{
        color = red;
        background-color = tomato;
    }
</style>
<body>
    <p class="class_name">
        <!--클래스 지정-->
        text
    </p>
</body>
```

-   한 요소에 여러 개의 클래스 지정도 가능하다. (공백으로 구분)

```html
<style>
    .class1 {
        color: tomato;
    }
    .class2 {
        background-color: red;
    }
</style>
<body>
    <p class="class1 class2">hello</p>
</body>
```

### inline block

-   display 프로퍼티를 이용하여 inline-block ... 등 여러 value를 지정할 때에 공간활용을 공평하지 못하게 분배한다는 문제점이 발생

-   즉, responsive design(반응형 웹디자인)을 지원하지 않는다.

-   이를 해결해주는 flexbox!

```html
<head>
    <style>
        p {
            display: inline-block;
            background-color: green;
            width: 200px;
            height: 200px;
        }
    </style>
</head>
```

-   위와 같이 스타일 및 display프로퍼티를 설정해 둔 후, 브라우저를 확대 - 축소 해보자.

    -   inline-block요소의 블록의 크기에 대해 자연스럽게 변하지 않고, 다음 줄로 넘어가버린다!

-   flexbox는 이에 대해 자동으로 공간을 계산하여 박사의 크기를 조절한다

### Flexbox Part one

-   주의 - **부모요소에만 flex임을 인지시키기**

-   부모 요소에 display프로퍼티를 flex로 지정한 뒤에는 해당 부모 요소에게 justify-content 프로퍼티 또한 적용할 수 있게 된다.

```html
<head>
    <style>
        body{
            display: flex;
            justify-content: center; <!--가운데맞춤-->
        }
    </style>
</head>
```

-   flexbox에는 축의 개념이 존재한다. 위의 justify-content 프로퍼티가 가로축(default)이고, align-items가 세로축(default)이다.

    -   flexbox에서 세로축은 main-axis, 가로축은 cross-axis이다.

    -   justify-content와 align-items가 가리키는 축의 방향이 각각 main과cross인 것은 기본 설정이고, 이는 바꿀 수 있는 옵션이다.

### flexbox part two

-   justify-content와 align-items가 가리키는 축의 방향을 바꾸고 싶을 때의 프로퍼티

```html
<style>
    body{
        display: flex;
        flex-direction: column; <!--or row-->
    }
</style>
```

-   main-axis가 수직이고, cross-axis가 수평일 때 -> column옵션

-   main-axis가 수평이고, cross-axis가 수직일 때 -> row옵션(default)

-   flex와 관련된 프로퍼티 지정은 **부모와 자식 관계** 에서만 적용되고, 부모의 부모에 있어서는 적용이 되지 않는다.

-   flex-wrap 프로퍼티 - 브라우저 사이즈에 따른 컨텐츠의 변화 지정

    -   nowrap -> 사이즈가 부족하면 그만큼 컨텐츠를 줄임

    -   wrap -> 사이즈가 부족하면 반응형에 맞추어 다음 줄로 넘어감

    *   wrap-reverse -> wrap될 때 x축 기준 대칭되어 쌓아올려짐

*   flex-direction 프로퍼티

    -   colunm-reverse : 나열된 컨텐츠들이 x축 대칭으로 변함

    -   row-reverse : 나열된 컨텐츠들이 y축 대칭으로 변환

#### CSS hack

-   **justify-content 프로퍼티의 space-between 값을 이용**

    -   flex로 나열된 컨텐츠들이 좌우로 공평하게 공간을 나누어 나열됨

    -   하지만 각 컨텐츠의 width에 따라 중앙의 컨텐츠가 좌 또는 우 방향으로 치우칠 수도 있다는 문제점이 발생

    -   css hack이용 !

```html
<style>
    body {
        display: flex;
        justify-content: center;
    }

    .myParentclass {
        width: 33%;
    }

    .myParentclass__column:nth-child(2) {
        display: flex;
        justify-content: center;
    }

    .myParentclass_column:last-child {
        display: flex;
        justify-content: flex-end;
        align-items: center;
    }
</style>
```

-   3분할된 공간을 공평하게 나누기 위한 작업.

### Fixed

-   position 프로퍼티 -> Fixed로 속성값 지정시 스크롤 해도 컨텐츠 고정.

-   참고) 스크롤 될 정도로 브라우저 내의 body 키우려면

    -   body 스타일에 height:1000vh (view height) 지정을 큰 값으로 !

### Relative absolute

-   position 프로퍼티의 default 값 -> static.

    -   레이아웃이 박스를 처음 위치하는 곳에 둠

-   position 프로퍼티의 relative

    -   속성값을 relative로 설정 시 top, bottom, left, right 프로퍼티를 사용할 수 있게 된다.

    -   element가 처음 위치한 곳을 기준으로 수정함.

```html
<style>
    div {
        width: 300px;
        height: 50vh;
        background-color: teal;
    }
    .class2 {
        background-color: blanchedalmond;
        height: 100px;
        position: relative;
        top: -10px;
    }
</style>
```

-   스타일 태그를 위와 같이 정의하고, body내에서 div가 중첩되어있는 구조이며 안쪽 div태그에 class2를 적용했다고 가정하자.

    -   position 프로퍼티를 relative로 설정하고 top bottom left right 프로퍼티중 원하는 것을 골라 속성값으로 -10px를 주면,

    -   안쪽 div 태그가 좌측 상단에 붙어있는 상황에서, 안쪽 div 박스가 10px 만큼 올라가게 된다.

    -   relative 단어의 의미답게 위치를 상대화 함으로써 처음 태그 생성 후 만들어진 요소의 위치로부터 적당한 간격으로 조절을 시도한다.

-   position 프로퍼티의 absolute 속성값

    -   가장 가까운 relative부모를 기준으로 이동한다.

    -   가정) body태그에 relative 속성을 주고, body내에 div태그를 중첩하여 두자.

    -   안쪽 div태그에 absolute속성을 주자

    -   자신의 부모 태그인 바깥 div태그는 relative가 아니므로 안쪽 div 태그에 right: 0px 프로퍼티를 설정하여도 바깥 div태그의 오른 쪽 끝으로 이동하지 않는다.

    -   가장 가까운 relative 부모인 body태그를 찾았고, 해당 body태그 공간의 가장 오른쪽 끝으로 가게 된다

### Pseudo Selector part one

-   Pseudo Selector란?

    -   세부적으로 셀렉터를 선택!

    1. 태그 이름
    2. 클래스
    3. id
    4. etc...

```html
<style>
    div:first-child{ <!--띄어쓰기 하면 안됨.-->
        color: black;
    }
    div:last-child{
        color: wheat;
    }
</style>
```

-   위의 예시를 보면, div: first-child 라는 표현을 썼음을 확인할 수 있는데, 이는 div태그들 중 가장 첫 번째 div태그를 말한다.

-   last-child의 경우 가장 마지막 div태그를 선택

-   nth-child도 존재한다.

    -   nth-child(odd,even,2n+1 .....)

```html
<style>
    div:nth-child(odd){
        color:tomato;
    }
```

### combinators

-   span 태그 전체에 style 적용하기

```html
<style>
    span {
        color: tomato;
    }
</style>
```

-   p 태그의 자식요소인 span 태그에 style적용하기

-   부모를 먼저 쓰고 자식 태그를 씀 -> 자식 태그를 부모 요소에서 찾음

-   children selector라고 부르며, 이를 지정 시 부모-자식의 구조가 맞지 않으면 스타일이 적용되지 않음.

```html
<style>
    p span {
        color: tomato;
    }
</style>
```

-   children selector 지정 시 생길 수 있는 문제

```html
<style>
    span {
        background-color: yellowgreen;
        padding: 5px;
        border-radius: 10px;
        text-decoration: underline;
    }
    p span {
        color: white;
    }
</style>
```

-   만약 위의 상황에서 p의 자식 요소의 span태그에는 underline 속성값을 주지않고, 바깥 요소의 span 태그에만 underline을 주고싶다면?

    1. span전체 태그에 text-decoration을 주고, p의 자식 요소에 text-decoration: none 을 준다. (좋은 방법 X)

    2. direct children을 지정한다. (부모 태그의 바로 밑 자식을 지정) ==> p > span{}

```html
<style>
    p > span {
        color: tomato;
    }
</style>
```

-   또한 p의 direct 자식을 지정하는 방법 외에 p의 형제 요소에 대한 스타일 지정 방법 또한 있다.

-   p + span{}의 형식을 지니면 p 다음에 오는 span태그에 대한 style을 지정하는 것이다.

```html
<style>
    p + span {
        color: tomato;
    }
</style>
```

### pseudo selectors part two

-   위의 combinator에서 +는 바로 다음 위치에 오는 태그에 대해서만 스타일이 적용된다는 한계가 있다.

-   이에 대해 ~ pseudo selector를 이용하면 형제관계가 바로 다음 위치에 오지 않아도 된다.

```html
<style>
    p ~ span {
        background-color: black;
    }
</style>
```

### Pseudo selectors part two

-   attribute selector

```html
<style>
    input[placeholder~="name"] {
        background-color: pink;
    }
</style>
```

-   태그 옆에 []를 통해 attibute selector를 설정할 수 있다.

-   이후 body태그에서 attribute selector를 호출할 수 있다.

    -   attribute_name = "Attribute value" -> 해당 속성을 지닌 태그를 제어

    -   attribute_name ~= "Attribute value" -> 해당 속성에 대한 단어를 포함한 모든 태그 제어

    -   attribute_name $= "Attribute value" -> 해당 속성에 대한 단어로 끝나는 모든 태그 제어

    -   등등.. 링크 참조

    [(특성 선택자 - attribute selector)](https://developer.mozilla.org/ko/docs/Web/CSS/Attribute_selectors)

```html
<style>
    a[href="https://google.com"]{
        color:green;
    }
    a[href$=".org"]{
        color:green;
    }
    a[class~="logo"]{
        color:red;
    }
    a[href*="example"]{
        color:wheat;
    }
```

### states

-   선택한 요소에 대해 특별한 상태이어야 만족하여 동작을 취함.

```html
<style>
    button:hover {
        color: red;
    }
</style>
```

[CSS States](https://developer.mozilla.org/ko/docs/Web/CSS/Pseudo-classes)

-   states 연계하기

```html
<style>
    form:hover input:focus {
        nackground-color: black;
    }
</style>
```

-   위와 같이 states를 연계하면 두 state를 모두 만족할 때 input 에 대해 제어한다는 의미이다. (form이 hover이고 input이 form 안에 있을 때)

### Recap

-   ::??

*   ::selection{} -> 커서 드래그를 통해 텍스트를 select 했을 때의 스타일 지정

```html
<style>
    p::selection {
        color: white;
        background-color: wheat;
    }
</style>
```

-   ::first-letter -> 첫 글자에 대한 스타일 지정

-   ::first-line -> 첫 줄에 대한 스타일 지정

### colors and variables

-   CSS color system

    1. hexadecimal color -> #F123

    2. RGB or rgba(a==투명도) -> rgb(197,93,161), rgba(195,32,132, 0.5)

-   같은 색을 여러 번 이용할 시 매번 복사&붙여넣기? NO!

    -   :root 엘리먼트를 추가 (모든 document의 뿌리가 됨)

    *   custom property!

    *   custom property는 색 뿐만 아니라 다른 것들도 저장 가능함.

```html
<style>
    :root {
        --main-color: #fcce00;
        --default-border: 1px solid var(--main-color);
    }
    p {
        background-color: var(--main-color);
    }
</style>
```

-   변수 명은 --var-name의 형식으로 선언해야하고, 호출 시에는 var(--var-name)으로 호출해야한다.
