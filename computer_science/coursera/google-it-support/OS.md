# What's an Operating System?

- SSH(secure shell)

  - protocol implemented(시행된) by other programs to securely access one computer from another.
  - 다른 컴퓨터에서 한 컴퓨터로 안전하게 액세스하기 위해 프로그램에 의해 구현된 프로토콜
  - protocol? 복수의 컴퓨터 사이나 중앙 컴퓨터와 단말기 사이에서 데이터 통신을 원활하게 하기 위해 필요한 통신 규약.
  - SSH를 사용하려면, SSH 서버에 연결하려는 컴퓨터에 SSH클라이언트가 설치되어있어야 함.
  - SSH 서버는 특정 기계가 아니고 소프트웨어임
  - 원격 시스템에서, SSH 서버는 background process로 실행되고있다. (background process -> 사용자 간섭 없이 보이지 않는 뒷편에서 실행 중인 컴퓨터 프로세스) -> **It constantly checks if a client is trying to connect to it, then will authenticate its requests.**
  - most popular program to use SSH -> 리눅스 내의 OpenSSH, 윈도우에서는 PuTTY

- SSH 사용

  - 원격 대상 컴퓨터에 계정이 있어야됨. + 해당 컴퓨터의 호스트 이름 or IP주소도 필요
  - the authenticity of host and then the IP address can't be established. 메세지의 출력 -> 이전에 이 컴퓨터에 연결한 적이 없고, SSH 클라이언트는 연결하려는 컴퓨터를 확인하거나 연결할 수 없다는 뜻
  - 메세지 출력 이후 올바른 원격 연결이면 yes -> 알려진 호스트로 저장되어 이후 메세지 출력 X
  - SSH를 통해 연결되었으므로 원격 장치에서의 텍스트 명령 입력 -> SSH 서버로 전달. (APP실행 가능, 셀 환경에서 작업대신 GUI를 통한 작업도 가능)
  - 비밀번호를 통한 SSH연결은 보안상 안전하지 않음. -> SSH 인증 키를 사용
  - SSH authentication key -> private key + public key
  - public key -> can only lock something, private key -> can only unlock something

- 원격 시스템에 연결 (2) -> VPN이용
  - VPN (virtual private network) - 멀리 떨어진 네트워크 환경을 안전한 네트워크로 만드는 역할
  - ex) 회사 내부에서만 접근가능한 네트워크를 집에서 접속하기 위해 VPN을 이용.

### Remote Connections on Windows

- PuTTY - SSH를 포함한 여러 네트워크 프로토콜을 통해 원격 연결을 할 수 있게 해주는 open source software

- PuTTY를 통해 컴퓨터 원격 연결하기

  1. PuTTY설치 및 GUI실행
  2. hostname, port, connection type options 기입
     - 포트 : SSH 프로토콜이 사용하는 기본 포트인 22로 설정됨
     - connection type은 SSH가 default
     - 실제 기입할 것은 host name or IP address (연결할 컴퓨터의 호스트 네임 또는 IP주소)

- GUI가 아닌 prompt상에서 실행하기

  - `putty.exe -ssh hostname@IPaddress 22`

- PuTTY Link (Plink)

  - PuTTY설치시 함께 내장되는 도구
  - Plink를 통해 SSH 원격 연결을 진행할 수도 있음.

- SSH는 windows기반 컴퓨터에서 Linux기반 OS에 연결할 때에 매우 유용

- SSH이외에 RDP(Remote Desktop Protocol)을 통해서도 컴퓨터 원격연결을 진행할 수 있음
- RDP client for Linux & MacOS는 real VNC와 Microsoft RDP on Mac과 유사하다.

  - VNC(Virtual Network Computing, RFB프로토콜 이용하여 컴퓨터 원격 제어)

- mstsc.exe

  - RDP연결을 만들기 위해 사용됨

- 시작 메뉴 -> 내 컴퓨터 우클릭 -> 속성 -> remote settings -> 보안 관련 설정 변경을 통해 원격연결 허용 가능
  - 원격 연결 허용 이후 컴퓨터에 접근 가능한 사용자 목록과 비교하여 존재하면 mstsc.exe를 통해 원격연결 가능

### Components of an Operating System

- What is OS?

  - Whole package that manages our computers resources and lets us interact with it.

- parts of OS

  1. kernel space
  2. user space

- kernel space

  - main core of an OS
  - 하드웨어와 직접 소통하고, 시스템 리소스를 관리함.

- what is system resource?

  > In computing, a system resource, or simply resource, is any physical or virtual component of limited availability within a computer system. All connected devices and internal system components are resources. Virtual system resources include files (concretely file handles), network connections (concretely network sockets), and memory areas.

- 컴퓨터 시스템 내에서의 물리적 또는 virtual한 구성요소

  - physical components -> all connected devices & interal system components
  - virtual components -> files, network connections, memory areas..

- user space

  - 사용자들은 커널 공간과 상호작용하지 않음
  - basically made up of everything outside the kernel

- Linux OS

  - open source여서, 전 세계의 개발자들이 이를 수정 및 공유하여 서로 발전시킴
  - 거기에 더하여 서로 다른 커뮤니티가 각자의 버전에 맞게 개발해낸 패키지가 존재함. -> Linus OSes distributions
  - Ubuntu, Debian, Red Hat등등이 이에 해당

- functions of kernel space
  1. file management : 파일을 관리 (디렉토리, 폴더)
  2. process management : 시스템상에서 실행하려는 파일들의 처리를 관리해줌
     - 실행 순서, 실행 리소스의 수, 실행 시간 등을 관리
     - process scheduler 가 멀티태스킹을 할 수 있게끔 도와줌. (실제로는 눈 깜짝할 사이에 프로세스의 전환이 이루어지는것)
  3. memory management : 메모리 사용 최적화 및 APP 구동에 필요한 메모리 할당량 확인
  4. I/O management (Input/Output) : 외부기기 (disk, 키보드, 네트워크 ,오디오 등)와 소통
     - 모든 입출력 관련된 작업을 수행 (파일 저장, 마우스 클릭, 마이크 출력 등)

* [Supplemental Reading for chorme OS](https://en.wikipedia.org/wiki/Chrome_OS)
  - chromium OS에서 파생
  - Linux distribution 중 하나인 Gentoo-Linux OS기반으로 google에서 디자인한 OS
  - chrome 브라우저 기반 UI
  - media player와 file manager를 통합
  - chrome apps -> 원격 액세스 지원
  - only available pre-installed on hardware from google manufacturing partners. (unofficial methods 도 존재)

### Files amd Files Systems

- 파일은 저장의 용이성 뿐만 아니라 **저장된 파일을 추적하는 것도 중요하다**
- kernel space에서 file stoarge와 file systems를 관리

- file system

  - 데이터 저장에 있어서 디스크를 지우고, 구성하는 일을 진행 (운영체제가 파일을 추적하는 방식)
  - file system의 종류에 따라 data storage의 양이 다르고, 속도 및 파일 손상에 대한 복원력도 다양함
  - 각 OS 업체에서는 고유한 파일 시스템을 권장
  - Windows file system - NTFS(Encryption,faster access speeds, security 등 다양한 기능 포함), ReFS도 있음 (개발중)
  - Mac OS file system - HFS+ (2017년 3월이후 APFS로 변경됨) - 저널링 기능(오류 발생시 디스크 상태를 저장 - 다른 OS file system에도 존재)
  - Linux file system - 각 배포판에 따라 다른 file system을 지님
    - 표준 리눅스 파일시스템 - ext4 (ext파일 시스템의 이전 버전도 사용가눙)
  - 다른 file system끼리는 파일이 정상적으로 처리되지 않음.

- storage of actual file data

  - 데이터 블록 형태로 하드 드라이브에 데이터를 저장
  - 하드 디스크에 저장할때에는 한 묶음으로 저장되는 것이 아님.
  - 이를 블록 스토리지라고 하고, 이를 통해 빠른 액세스가 가능하여 데이터 처리 속도가 향상됨 + 스토리지 공간 활용의 효율성 증대

- metadata

  - 파일에 대한 정보를 담고있는 metadata를 유지해야함 (kernel공간의 file system이)
  - 파일 작성자, 최종 수정일, 누가 파일에 접근 가능한 지 등 + 파일 형식

- [supplemental readings for ReFS](https://en.wikipedia.org/wiki/ReFS)

### Process management

- Process vs Program

  - Process - program that's executing (internet browser or text editor)
  - Program - application that we **can run**

- 프로그램의 구동을 위해서는 CPU와 RAM이라는 리소스를 투입해야하는데, 다양한 프로세스를 동시에 처리함에 있어서 효율성을 증대시키기 위해 kernel이 존재한다.
- 프로그램 실행을 위해서는 프로세스를 만들어야함. 이러한 프로세스는 RAM 및 CPU같은 리소스가 필요
- 하나의 CPU에 여러 프로세스를 처리하기 위해서 커널이 **time slice**를 통해 실행

  - time slice : very short interval of time that gets allocated to a process for CPU execution (CPU실행을 위해 프로세스에 할당되는 짧은 시간)

- 프로세스에 할당된 time slice가 CPU가 일반적으로 처리하는 time slice보다 클 경우 또는 처리할 프로세스가 너무 많을 경우 컴퓨터가 느려짐 -> 수동 관리 필요

### Memory Management

- 프로세스의 실헹에는 CPU에 할당되는 time slice도 필요하지만, 메모리도 필요하다.
- 하드 드라이브와 비교하면 메모리는 작은 양을 지니기 때문에, 더 많은 메모리를 제공하기 위해 virtual memory라는 개념을 도입한다.

- virtual memory? : combination of hard drive space and RAM that acts like memory that our processes can use.

- process의 실행시 프로그램 데이터를 page라고 불리는 chunks(데이터 덩어리)로 가져온다.
  - 이러한 페이지들을 virtual memory에 저장
  - 페이지들을 read and execute하고싶으면 RAM으로 보내야함.
  - hard drive에 virtual memory를 저장하려면, swap space라는 할당된 공간에 저장해야함. (RAM의 용량이 꽉 차게 되었을 때 이용)
  - [스왑공간이란?](http://coffeenix.net/doc/RH-DOCS/rhl-cg-ko-9/ch-swapspace.html)

### I/O management

- I/O devices : devices that perform input and output (monitors, mice, hard disk, network adapter..)
- I/O 장치들은 커널에 의해 관리되고, 각 장치들의 드라이버를 로드하여 서로 다른 하드웨어끼리 소통할 수 있게해줌

### interacting with the OS : User Space

- two ways that we can interact with our OS

  1. shell환경
  2. GUI환경 (GUI기반 shell도 있지만 대부분 CLIA shell을 주로 이용 - Command line interface)

- shell? : program that interprets text commands and sends them to the OS to execute.
  - power user(시스템 관리자 및 사용자가 각종 전자기기를 다룰 때 일반 수준을 넘어서는 기술력을 가진 사람) 가 주로 shell환경을 이용
  - 다양한 shell이 존재. (windows - Powershell, Linux - Bash(Bourne Again Shell)..)

### The Boot process

- 컴퓨터의 시작 -> 부팅
- 많은 OS들은 일반적인 패턴을 따른다.
  1. computer is powered on
  2. BIOS/UEFI에서 하드웨어 초기화 및 정상작동 점검 이후 POST진행 (Power on Self Test, 컴퓨터 정상 작동여부 확인. 진단 테스트 진행)
  3. BIOS/UEFI구성에 따라 부팅 디바이스 선택 (부팅 순서에 따라 선택됨. 하드 드라이브 -> USB -> CD드라이브 등)
  4. 부팅 디바이스 선택을 위해 각 디바이스들을 검사할때, Bootloader를 검색함.
     - Bootloader? : small program that loads the operating system
  5. bootloader실행 -> 더 크고 복잡한 프로그램들이 로드 -> OS로드

### Choosing an Operating System

- [Which Operating System Should You Choose for Your Next PC?](https://www.makeuseof.com/tag/operating-system-choose-next-pc/)

1. Windows
   - 가장 일반적인 OS로, 호환성이 좋음
   - 고사양 게임에 최적화
   - 보안이슈가 여전히 존재 (malware) - 소프트웨어 업데이트에 신경써줘야함
2. MacOS
   - only available on Mac hardware. (맥 기기가 아닌 곳에도 설치 가능 - Hackintosh, 복잡함)
   - 특정 소프트웨어는 크로스플랫폼이더라도 맥에서 더 많은 옵션을 제공하는 경우가 존재. (전문가들에게 좋음) - Adobe photoshop or premier
   - MacOS 소프트웨어 업데이트가 무료임 & 맬웨어 공격대상으로 잘 지정되지 않음
   - 맥 기기가 비쌈 & 소프트웨어 호환성문제
3. Linux
   - flexibility가 가장 큰 장점
   - 복잡한 작업을 진행하는 데에 있어서 power user들에게 자유도를 부여
   - 리눅스 러닝 커브가 가파름
   - 오래된 하드웨어도 돌아가게 해줌 (windows 실행에 무리가 있는 하드웨어도 경량 linux배포판 설치 이후 간단한 작업 가능)
4. Chrome OS
   - chrome web browser, chrome apps, Android Apps에 접근 가능
   - Windows desktop software는 실행 불가
   - 매우 간단하기 때문에 랩탑에 잘 맞음.
5. BSD
   - Linux의 대체재 - Berkeley software distribution
   - Unix-based & open source
   - 보안 및 복잡한 네트워킹 작업에 이용됨
   - 리눅스보다 flexible
   - 써드파티의 규모가 작아 troubleshooting이 쉽지않음

### Linux OS

- [Ubuntu site](https://ubuntu.com/)
- [etcher.io](https://www.balena.io/etcher/)
  - USB에 설치 이미지파일을 로드해주는 툴
- [Ubuntu update](https://www.ubuntuupdates.org/)
- [Ubuntu Unity is dead: Desktop will switch back to GNOME next year](https://arstechnica.com/information-technology/2017/04/ubuntu-unity-is-dead-desktop-will-switch-back-to-gnome-next-year/)
  - GNOME - Linux GUI환경
  - Ubuntu 보급회사인 canonical이 Unity를 Ubuntu 데스크톱의 default UI로 만든 지 6년만에 이를 그만두고 GNOME으로 전환할 예정
  - 모바일 시장으로의 적응에 실패했지만, IoT 및 cloud + Infrastructure부문에 투자중
