# bootstrap collapse

-   부트스트랩의 collapse를 통해 토글 애니메이션을 구현할 수 있다.

1. bootstrap에서 요구하는 링크들을 모두 import한다.
2. 동작을 지시할 태그에 프로퍼티로 `data-bs-toggle="collapse" data-bs-target="#target"` 두가지를 추가해준다.
3. 동작을 받아서 숨겨졌다가 다시 나타날 대상에 대해 id프로퍼티로 동작 지시 프로퍼티에서 `data-bs-target="#target"`으로 지시했던 target이라는 아이디를 이용한다.

-   동작 지시 태그가 button 및 a태그에만 해당하는 지는 확인필요

```html
<head>
    <link
        href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.1/dist/css/bootstrap.min.css"
        rel="stylesheet"
        integrity="sha384-+0n0xVW2eSR5OomGNYDnhzAbDsOXxcvSN1TPprVMTNDbiYZCxYbOOl7+AMvyTG2x"
        crossorigin="anonymous"
    />
</head>
<body>
    <div>
        <button data-bs-toggle="collapse" data-bs-target="#collapseTarget">
            Button
        </button>
        <p class="collapse" id="collapseTarget">Hide on bush</p>
    </div>
    <script
        src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.1/dist/js/bootstrap.bundle.min.js"
        integrity="sha384-gtEjrD/SeCtmISkJkNUaaKMoLD0//ElJ19smozuHV6z3Iehds+3Ulb9Bn9Plx0x4"
        crossorigin="anonymous"
    ></script>
    <script
        src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.9.2/dist/umd/popper.min.js"
        integrity="sha384-IQsoLXl5PILFhosVNubq5LC7Qb9DXgDA9i+tQ8Zj3iwWAwPtgFTxbJ8NT4GN1R8p"
        crossorigin="anonymous"
    ></script>
    <script
        src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.1/dist/js/bootstrap.min.js"
        integrity="sha384-Atwg2Pkwv9vp0ygtn1JAojH0nYbwNJLPhwyoVbhoPwBhjQPR5VtM2+xf0Uwh9KtT"
        crossorigin="anonymous"
    ></script>
</body>
```
