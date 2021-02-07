# HTML 기초 문법

### HTML Tag

-   브라우저는 생각보다 멍청하기 때문에</br> 프로그래머가 태그를 마음대로 정의하여도</br>이에 대한 실질적 행위가 이루어지지 않는다.</br></br>

```html
<greet>HI</greet>
```

<img src = "/html.png" width="100%" height="100%"></img>

-   만약 greet이라는 태그가 실제 있는 태그였다면 </br> **브라우저가 HI 라는 텍스트를 greet태그에 대한 특정 행동으로 인식했을 것이다.**</br>

---

### More Tags

-   Tag 관련되어 구글링할 때에</br></br> **keyword mdn**</br></br> 키워드 뒤에 **mdn**을 반드시 추가하자.</br> (Mozilla Developer Network의 약자로, 태그들에 대한 정보를 참고하기 좋은 사이트)</br>

### Tag Attributes

```html
<img src="" />
<!-- src속성값으로 상대경로를 통한 파일에 직접접근, 인터넷링크를 통한 접근이 가능하다.-->
```

-   HTML 기본 작성 구조

```html
<!DOCTYPE html>
<html>
    <head>
        <!--웹사이트 환경 조성!-->
        <!--title태그가 그 예시가 될 수 있음-->
        <title>myhtml</title>
    </head>

    <body>
        <!--사용자가 직접 볼 수 있는 contents 표시.-->
    </body>
</html>
```

-   HTML의 기본적인 작성 구조는</br>맨 처음 !DOCTYPE html을 통해 앞으로 작성할 코드들이 </br>단순 text가 아니라 html문서임을 브러우저에게 알리고,</br></br>**head 태그를 통해 웹사이트의 환경, page의 환경을 조성**하며</br></br>**body태그를 통해 사용자가 볼 수 있는 컨텐츠들을 표시한다.**</br></br>쉽게 말해, 페이지 상에 보이는 거의 모든 것들은 body태그 내에 작성된다고 생각하면 된다.</br></br>head태그 내에 컨텐츠 표시에 대한 코드를 작성한다고 해도</br>오류가 발생하지는 않지만 특정한 변화도 생기지 않는다.</br></br>**head에서 이해하는 동작과 body에서 이해하는 동작이 따로 있기 때문!**</br>

---

### More Tags

-   head 태그 내에 입력하는 태그들 중</br>**meta**태그라는 것이 있다.</br></br>해당 태그가 하는 일은</br>부가적인 정보들을 웹 환경에 반영하는 역할을 한다.</br>

```html
<head>
    <meta charset="utf-8" />
    <meta lang="en" />
</head>
```

-   예시로, meta 태그의 속성으로 charset,lang을 들 수 있다. </br>charset은 텍스트 인코딩을 지정하여</br>한글표시 및 특수문자가 깨지지 않도록 해주고</br></br>lang은 웹에 표시할 언어를 지정해준다.</br></br>

### More Tags and IDs

```html
<!DOCTYPE html>
<html>
    <head>
        <style>
            #first {
                color: teal;
            }
            #second {
                color: tomato;
            }
        </style>
    </head>

    <body>
        <div id="first">hello</div>
        <div id="second">hello2</div>
    </body>
</html>
```

-   중복되는 태그 div 두개가 있다는 것을 위의 코드에서 확인할 수 있다. </br></br>특정 div에만 프로그래머가 원하는 속성을 정하고 싶을 때 id를 이용한다.</br></br>주의할 점은,</br></br>

1. style태그 내에서 해당 id에 대한 접근 시 해시태그# 를 이용해야 하며
2. 당연하게도 body에서 지정할 id와 해시태그의 id는 동일해야하고
3. **한 요소당 하나의id만 등록 가능하다** (div하나에 다수의 id 등록 불가) **unique해야 한다는 속성**
4. id를 unique identifier라고도 한다.</br>

---

### Semantic HTML

-   MDN에서 나타내는 Semantic tag에 대한 정의

    > 프로그래밍에서,시맨틱은 코드 조각의 의미를 나타냅니다 — 예를 들어 ("이게 어떻게 시각적으로 보여질까?" 보다)"이 Javascript 라인을 실행하는 것은 어떤 효과가 있는가?", 혹은 "이 HTML 엘리먼트가 가진 목적이나 역할은 무엇인가?"

-   div 태그는 division, 즉 공간에 대한 구획의 기능으로</br>위치에 대한 지정을 해주는 태그이다.</br></br>해당 태그가 의미론적으로는 의미가 없다.</br>즉 태그 자체로 자신의 컨텐츠에 대한 설명을 하지 않는다.</br></br>이런 것들을 **Non-semantic tag**라고 한다.</br></br>반면 **semantic tag**의 예시를 보면</br>header태그를 들 수 있는데,</br></br>이는 **header태그를 HTML문서에서 보기만 해도 해당 태그가 웹사이트의 header, 즉 제목과 관련된 부분임을 미루어 짐작할 수 있다는 것**이다.</br></br>공간의 구획 기능을 한다는 점에서 </br>header,main,footer태그를 모두 div태그로 대체 가능하지만</br></br>**HTML 문서를 이해하는 데에 있어 어려움이 있기 때문에 </br>코드를 항상 semantic하게 작성하기 위한 노력을 해야한다**</br>

[HTML Semantic Tag - mdn content sectioning part 참조.](https://developer.mozilla.org/ko/docs/Web/HTML/Element#%EC%BD%98%ED%85%90%EC%B8%A0_%EA%B5%AC%ED%9A%8D)
