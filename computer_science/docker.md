# docker란

-   [노마드코더 - Docker가 왜 좋은지 5분만에 설명해줌](https://www.youtube.com/watch?v=chnCcGCTyBg)
-   docker는 environment disparity 문제를 해결해줌.
-   **environment disparity** ex) 컴퓨터환경은 windows, 서버 환경은 linux여서 서버로 올린 코드가 작동하지 않는 상황
    -   컴퓨터 환경에 따라 모든 서버를 구축해야하는가? - 비효율

### Docker 작동

1. 서버와 컴퓨터에 Docker 설치
2. docker파일 생성 및 구현환경 설정 (우분투, 깃, 파이썬 등)
3. 설정한 파일을 서버와 컴퓨터 모두에게 줌
4. docker가 해당 설정한 환경과 같은 버츄얼 컨테이너를 (우분투+..) 컴퓨터에 만듦
5. docker가 서버에 필요한 것들도 다운받아줌

-   docker의 각 컨테이너들은 독립적.
-   한 개의 서버에 각기 다른 많은 컨테이너를 가질 수 있게 됨
    -   파이썬 컨테이너
    -   node.js 컨테이너
    -   java 컨테이너 등..
-   java트래픽이 늘어남 -> java컨테이너 늘리기.. (서버의 추가X)

-   **컨테이너란?** - 어떤 환경에서나 실행하기 위해 필요한 모든 요소를 포함하는 소프트웨어 패키지
