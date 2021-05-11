# Module Introduction

## The Modern Computer

### Introduction to Computer Hardware

-   모니터, 키보드 등.. 물리적 구성요소들을 통틀어 하드웨어라 칭함

-   ports? - Connection points that we can connect devices to that extend the functionality of our computer

-   CPU(Central Processing Unit) : The brain of our computer, it does all the calculations and data processing.

-   RAM(Random Access Memory) : Our computer's short-term memory

-   Hard drive : Holds all of our data, which includes all of our music, pictures, applications.

-   Motherboard : It holds everything in place and lets our components communicate with each other. -> foundation of computer

    -   The body of circulatory system of the computer that connects all the pieces together.

-   power supply : Converts electricity from our wall outlet onto a format that our computer can use.

### Programs and Hardware

-   Programs - Instructions that tell the computer what to do
-   인간이 컴퓨터와 소통하기 위해서는 인간의 언어를 machine language로 번역해야함! (Binary)

-   RAM에 대한 설명

*   **RAM is memory that is randomly accessed, allowing our CPU to read from any part of RAM as quickly as any other part.** - 램은 자신의 어떤 부분에서든지 CPU가 다른 컴포넌트만큼 빠르게 읽을 수 있는 랜덤 액세스 메모리
    1. 요리를 위해 요리사를 고용 (CPU)
    2. 요리사가 처리하기 용이한 요리에 대해서는 쿡북을 읽으며 요리하는 것보다 혼자 요리하는 것이 더 빠름(RAM)
        - "Remember that RAM is our computer's short-term memory. It stores Information in **a location our CPU can access faster than it could with our hard drive.**
    3. 요리사에게 요리 레시피를 골라 전달하는데, 효율적인 instructions 전달을 위해 각 순서에 따라 한 라인씩 전달한다. (one line at a time) + 요리사에게 전달하는데, 요리사가 알아먹는 형식은 Binary형식이므로, 변환하여 전달해야한다. (복잡한 과정. ) => "Our CPU is constantly taking Instructions and executing them."

-   EDB - External Data Bus

    -   It's a row of wires that interconnect the parts of our computer, kind of veins in our body.
    -   EDB를 통해 voltage(전압)을 보내면 1, 없으면 0임.(on&off)
    -   즉 byte는 EDB를 통해 컴퓨터 내부에서 움직인다.
    -   EDB는 다양한 사이즈가 존재한다. (8bit, 16,32,64까지도 존재)
    -   8bit EDB를 가정하고, 1바이트 데이터를 CPU에 전달하는 상황
        -   CPU 내부의 레지스터가 CPU가 받은 데이터를 저장할 수 있게 해줌
        -   1+2=3을 저장 -> 1이 register a, 2가 register b, 덧셈의 결과인 3이 register c에 저장.

-   MCC - Memory Controller chip

*   [What is the Memory Controller?](https://www.easytechjunkie.com/what-is-the-memory-controller.htm)

    -   HDD로부터 전달된 RAM의 데이터는 너무 방대하기때문에, EDB를 통한 1바이트 통신에 더하여 또 다른 컴포넌트의 도움이 필요하다. MCC!
    -   MCC는 CPU와 RAM 사이의 다리와 같은 역할을 함

    *   **It manages read and write operations with system memory, along with keeping the RAM active by supply the memory with electric current.**

*   Address bus

    > 주소 버스(address bus)는 일정한 메모리 번지를 찾는 데 사용되는 신호를 운반하는 컴퓨터 내의 배선 버스이다. 간단히 말해 물리 주소를 지정하는 데 쓰인다.

*   주소 버스는 CPU와 MCC를 연결하여 주소를 주고받는다. (데이터 자체를 주고받는 것이 아님.)

*   **정리**

1. CPU의 데이터 요청
2. HDD로부터 RAM에 데이터가 전달됨
3. CPU가 요청한 데이터에 대해 MCC가 Address bus로부터 데이터 주소를 받아와 EDB를 통해 CPU에 전달.
4. 데이터 접근 후 처리

-   [한빛 미디어 - 뇌를 자극하는 윈도우즈 시스템 프로그래밍 中 버스부분 발췌](https://www.youtube.com/watch?v=bGPYyVAXG9I&list=PLVsNizTWUw7E2KrfnsyEjTqo-6uKiQoxc&index=2)
-   CPU와 RAM 데이터 이동에서의 버스 시스템

    1. 데이터 버스 - 데이터가 이동
    2. 어드레스 버스 - 데이터 주소의 이동
    3. 컨트롤 버스 - 컨트롤 신호의 이동 (CPU와 RAM 사이의 데이터 이동은 양방향임을 기억하자)

-   Cache

    -   RAM은 CPU입장에서 데이터 처리 속도가 그렇게 빠르지 않다. (RAM 내부의 트랜지스터가 on 되려면 off에서 충전되어야함)
    -   따라서, 자주 사용되는 데이터를 CPU 캐시 메모리에 저장하여 빠르게 접근한다.
    -   CPU 내부에서 cache level은 L1, L2, L3로 쪼개진다.
    -   L1 -> 가장 작고 가장 빠름

-   CPU clock
    -   [What is CPU clock?](https://www.quora.com/What-is-a-CPU-clock)
    -   "CPU clock is for measuring the speed of processor."
    -   CPU 클럭은 clock wire에 연결되어있다.
    -   데이터를 전송하거나 전달받을때, clock wire에 전압을 보내 CPU가 계산을 시작할 것이라는 것을 알림.
    -   voltage가 clock wire로 보내지는 한 단위가 clock cycle이다.
    -   CPU 속도를 표기할 때에 3.4ghz로 말하는 것은 clock cycle이 초당 34억회 진행된다는 것(Maximum, 항상 이러한 속도로 사이클이 돈다는 것 X)
    -   CPU maximum clock cycle을 초과할 수도 있는데, 이를 **CPU Overclock이라고함.** - "in order to perform more tasks."
    -   빡센 게임을 돌릴 때 발생한다고 생각하면 됨 (CPU에 발열이 발생)
