# Introduction to IT

### Digital Logic

##### Character Encoding

-   웹 및 어플리케이션상에서 모든 문자들이 0과 1로 렌더링 되는 것은 매우 불편한 일
-   이를 해결하기 위해 0과 1로 이루어진 이진수들의 조합을 각 문자에 매핑하여 컴퓨터가 인식할 수 있도록 한 테이블이 등장 - **ASCII**

-   ASCII는 1바이트의 모든 경우의 수인 256개 중 127개만을 사용하여 표현할 수 있다는 것이 장점.
    -   하지만 이후 다양한 문자에 대해 이진수 조합을 매핑하기 위해서는 1바이트 하나의 조합으로는 부족함
    -   **UTF-8**이 등장. -> 동일한 ASCII테이블과 함께 다양한 바이트 수를 이용하여 매핑
    -   UTF-8을 통해 한 바이트 이상의 문자로 문자를 저장할 수 있게됨
    -   Unicode standard를 따라 문자의 인코딩을 일관된 방식으로 진행

##### Binary

-   과거 punch card를 통해 컴퓨터가 데이터를 인식
-   현재 -> 트랜지스터 전기 신호의 통과 여부를 통해 0과 1의 상태 인식

-   **Logic gates** - Allow our transistors to do more complex tasks, like decide where to send electrical signals depending on logical conditions
-   [Detail information of Logic gate](https://simple.wikipedia.org/wiki/Logic_gate)

##### How to Count in Binary

-   128 + 64 + 32 + 16 + 8 + 4 + 2 + 1 = 255 -> 1바이트 상에서 10진수 표현할 수 있는 최대값은 255.
-   01101000 -> 2^6 + 2^5 + 2^3 = 104 . On & Off 형태라는 것을 생각하며 2진수 변환하기

### Computer Architecture Layer

##### Abstraction

-   CS에서는 Abstraction이라는 개념을 자주 사용한다.
    -   하드웨어 및 소프트웨어가 상호작용하는 원리를 자세히 알지 못해도 사용자 입장에서는 불편함이 없다.
    -   추상화를 통해 공통적인 인터페이스에 대해 복잡성을 숨겨 사용자로 하여금 편한 이용을 할 수 있게 해줌.

##### Computer Architecture Overview

-   Abstraction을 통해 **사용자 입장에서** 컴퓨터에 대한 복잡성이 줄어든 것은 맞지만, CS를 직접 활용해야하는 우리 입장에서는 컴퓨터 구조의 모든 layer들을 파악해야한다.

-   Computer Architecture layer
    1. Hardware
        - 물리적 요소 - 랩탑, phone, 모니터, 키보드 등
        - 작동방식에 대한 이해
    2. os
        - 하드웨어와 시스템의 소통을 위해 만들어짐.
    3. Software
        - 사람과 컴퓨터 사이에 상호작용하기 위함
        - 모바일 앱, 브라우저, OS 등..
        - 소프트웨어의 설치, 다양한 타입의 소프트웨어와 상호작용하는 방식에 대해 이해
    4. Users
        - CS를 실제적인 issue에 어떻게 적용하는 가에 대한 방법론
        - 문제 해결 전략에 대한 탐색
