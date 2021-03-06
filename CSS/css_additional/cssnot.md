# CSS not, cursor 프로퍼티, color 상속, form action&method, navigation

```html
<style>
    #login-form input:not([type="submit"]) {
        border-bottom: 1px solid rgba(0, 0, 0, 0.2);
    }
</style>
```

-   위의 예시의 경우, [ type="submit" ]은 특성 선택자(attribute selector)이고, input type이 submit이 아닐 때에만 아래의 프로퍼티들이 적용될 것이라는 뜻.

### cursor 프로퍼티

-   cursor 프로퍼티에는 progress pointer not-allowed 등이 있다.

-   위의 예시를 통해 특성 선택자 이용 -> cursor property 이용

### color 상속

```html
<style>
    #login-form a {
        text-align: center;
        color: inherit;
    }
</style>
```

-   color프로퍼티에 inherit 값을 주면 부모로부터 색을 상속받는다.

### form action attribute, method attribute

-   action -> 어떤 페이지로 data를 보낼 것인지 지정

-   method -> POST & GET

    -   POST -> 백엔드 서버에 정보를 전송하는 방식

    -   GET -> 보안에 취약 (URL에 포함되어도 상관없는 정보를 보냄)

```html
<form method="get" action="name.html"></form>
```

### navigation

-   navigation태그는 일반적으로 ul로 나눠지고, 그 안에 많은 li로 구성

```html
<nav>
    <ul>
        <li>
            <a href="#"></a>
        </li>
    </ul>
</nav>
```
