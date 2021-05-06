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
