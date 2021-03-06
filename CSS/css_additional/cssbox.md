# box-sizing, text-transform, z-index, flex children 순서변경, forwards animation, will change

### box-sizing

-   특정 block에 padding-left:50px를 지정했다고 가정

    -   프로그래머가 block에 width를 지정한 상황이라면 (200px) -> 200px을 유지하기 위해 padding만큼 block을 늘리게 된다.

    -   이를 방지하기 위해 box-sizing을 이용 -> **CSS에게 box size를 바꾸지 말라고 알려줌**

-   box-sizing:border-box -> content가 보일 부분을 늘리지 않음

### text-transform

-   html상에서 영문의 소문자 및 대문자도 디자인적 요소이기 때문에 태그를 통해 변환할 수 있다.

```css
.open-post__hashtags {
    text-transform: uppercase;
}
```

### z-index

-   z-index를 통해 layer 순서를 정함.

*   z-index 설정을 통해 스크롤시 position absolute로 설정되어 있는 컨텐츠가 투과되어 보이는 현상을 방지할 수 있다.

```css
.nav {
    position: fixed;
    bottom: 0;
    width: 100%;
    background-color: #f9f9fa;
    padding: 20px 50px;
    box-sizing: border-box;
    border-top: 1px solid rgba(124, 124, 124, 0.3);
    <!-- z-index: 1; -->
}
```

<img src="../images/zindex.png" height="100px" width="100px"/>

<img src="../images/zindex2.png" height="100px" width="100px"/>

### flex children 순서변경

```css
.parent {
    flex-direction: row-reverse;
}

.parent .children {
    order: 1;
}
```

1. 부모를 flexbox로 만든 후 자녀 태그들의 순서를 reverse를 통해 거꾸로 바꿈

2. flexbox인 children태그들을 order를 통해 직접 순서 지정해줌

### forwards animation

-   keyframes로 정의한 애니메이션의 경우 from ~ to에서 to까지 애니메이션을 진행한 뒤에 가장 처음 상태로 되돌아 간다.

-   splash screen 구현을 위해 animation 마지막에 forwards속성을 추가하면 to 상태를 계속 유지하게 된다.

```css
@keyframes hideSplashScreen {
    from {
        opacity: 1;
    }
    to {
        opacity: 0;
    }
}

#splash-screen {
    animation: hideSplashScreen 1s ease-in forwards;
}
```

-   하지만, **element가 완전히 살아지는 것은 아니므로, 덮어씌워진 밑의 element들을 사용할 수 없게 되는 문제점이 발생**

-   따라서, visibility:hidden을 이용 (브라우저가 element를 무시하기 위한 기술 -> 완전히 없애기 위해서는 JavaScript를 이용)

### will-change

* 브라우저에게 무엇인가 바뀔거라고 전달하기 위한 property

* 애니메이션을 더 낫게 만들어줌