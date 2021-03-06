# Software

## Introduction to software

### What is software?

-   software terms
    1. coding : translating one language to another
    2. Scripting : coding in a scripting language
        - scripting language : mainly used to perform a single or limited range task.
    3. programming : coding in a programming language
        - programming language : special languages that software developers use to write instructions for computers to execute

### Types of software

-   Commercial vs non-commercial software

    1. commercial - licence 구입
    2. non-commercial - making it open source
        - developers will let other developers share, modify, and distribute their software for free.

-   software that is categorized by function

    1. application software : fulfill a specific need - text editor, web browser, graphics editor...
    2. system software : used to keep our core system running - OS tools and utilities
    3. Firmware : Permanently stored on a computer component (BIOS)

-   software versions

    -   versions are tell us what features were added to a specific software iteration
    -   [What is iteration?](https://searchsoftwarequality.techtarget.com/definition/iteration)
    -   In agile software development, an iteration is a single development cycle, usually measured as one week or two weeks. An iteration may also be defined as the elapsed time between iteration planning sessions.
    -   elapsed time : amount of time that passes from the start of an event to its finish.
    -   standard that distinguish a version : sequential numbering trend.
        -   1.2.4 -> 1.3.4

-   agile software development (애자일 방법론)

    -   [애자일 소프트웨어 개발](https://ko.wikipedia.org/wiki/%EC%95%A0%EC%9E%90%EC%9D%BC_%EC%86%8C%ED%94%84%ED%8A%B8%EC%9B%A8%EC%96%B4_%EA%B0%9C%EB%B0%9C)
    -   프로젝트의 생명주기동안 반복적인 개발을 촉진한다.
    -   소프트웨어 개발 방법론에 있어서, 아무런 계획이 없는 방법론 vs 지나치게 디테일한 개발 방법론 사이의 타협점 (계획이 없는 -> 미래에 대한 예측이 힘듦, 지나치게 디테일한 -> 형식적 절차를 따르는 데 필요한 시간 & 비용 + 개발 흐름 자체를 느리게함)
    -   less document-oriented, more code-oriented
    -   예측하며 개발 X -> 일정한 주기를 가지고 끊임없이 프로토타입을 만들어냄.

-   [software versioning](https://en.wikipedia.org/wiki/Software_versioning)
    -   Definition : process of assigning either _unique names_ or unique _version numbers_ to unique state of computer software.
    -   At a fine-grained level (세분화된 수준), revision control(==version control, source control) is often used for keeping track of incrementally different versions of information, whether or not this information is computer software. (버전 컨트롤은 정보에 대한 점진적 변화를 추적하는 데에 사용하는데, 해당 정보가 세분화된 수준에서는 컴퓨터 소프트웨어에서만 국한된 의미가 아님.)

> Modern computer software is often tracked using two different software versioning schemes—internal version number that may be incremented many times in a single day, such as a revision control number, and a release version that typically changes far less often, such as semantic versioning or a project code name.

-   현대 소프트웨어는 두 가지 버전관리체계로 분류됨. (two different software versioning schemes)

    1. internal version number : 배포 이전 자주 바뀔 수 있는 체계
    2. release version : semantic versioning or project code name

-   [what is semantic versioning?](https://velog.io/@iamjoo/Semantic-Versioning%EC%9D%B4%EB%9E%80)
    -   Major.Minor.Patch (1.1.1 이런식으로 이루어짐)
    -   Major : breaking change
    -   Minor : backwards compatible new functionality, old functionality deprecated (but operational - 이전의 기능이 더이상 사용되지 않지만 작동은 가능), large internal refactor(리팩토링 - 외부 동작에 변화는 없지만 내부 구조의 개선)
    -   Patch : bug fixes

### Recipe for Computing

1. Assembly language
    - punch cards를 통해 일련의 컴퓨팅 연산을 지시하던 것에 많은 피로감이 존재함. -> Assembly 언어의 개발
    - human readable instructions, assembled into code that the machines could understand. Instead of generating binary code, computer scientists could program using machine instructions. (Add 1, Add 2....)
    * 제아무리 human readable한 언어로 사용되었다고 하더라도, 여전히 기계적이었고 **특정 CPU에서 작성된 것은 해당 CPU에서만 또는 해당 CPU의 제품군에서만 구동될 수 있었다.** -> Compiled programming language의 개발 동기
2. Compiled programming language
    - uses human readable instructions, then **sends them through a compiler**
3. Interpreted languages
    - aren't compiled ahead of time. (미리 컴파일 되지 않음)
    - Interpreted language로 작성된 파일 -> Script라고 불림
    - The script is run by an interpreter, which interprets the code into CPU instructions just in time to run them.
