## CSS textarea 크기 조절 안되게 막기

-   textarea 기본 세팅은 우측 하단에 크기 조절이 가능하도록 되어있는데, 이러한 기능을 끌 수 있음

```css
textarea {
    resize: none;
}
```

## CSS autocomplete

-   input에 autocomplete속성값을 off로 주면 자동완성추천 기능을 끌 수 있다

```html
<input autocomplete="off" />
```

## DIV 영역 자체에 링크 걸기

```html
<!-- cursor: pointer를 통해 꾸미는 것은 자유 -->
<div onclick="location.href='URL';"></div>
```

-   블로그에 적용한 예제

```html
<div
    class="main_bar--link"
    onclick="location.href='https://github.com/Parkjju'"
>
    <p>Github</p>
</div>
```

1. 현재페이지에 부르기 `onclick="location.href='URL'"`
2. 새 창에 부르기 `onclick="window.open('URL')"`
