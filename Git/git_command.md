# Git 명령어 정리(계속)

```bash
$git add filename
```

-   git에서 관리할 파일을 추가하는 명령어</br></br>

```bash
$git commit -m "message"
```

-   소스 코드 일부의 최신 변경사항을 추가해</br>저장소의 최상위 기록으로 만드는 과정

-   메세지의 내용으로 "Add: ~" "Update: ~" "Modified ~" 등 관례적 사용 형태가 있다.</br></br>

```bash
$git log
```

-   커밋 로그 조회하기</br></br>

```bash
$git remote add origin "url"
```

-   원격 저장소 연결</br></br>

```bash
$git push -u origin main
```

-   github에 커밋 push하기

-   git push명령을 통해 origin (Github에 만든 저장소)의 main브랜치에 커밋 내용을 반영</br></br>

```bash
$git pull
```

-   git push하였던 로컬 저장소에 진입한 상태에서</br>github 원격저장소에서 추가한 새로운 내용들을 가져오는 명령어.</br></br>

```bash
$git clone
```

-   git clone 명령어를 통해 원격저장소의 주소 복제 및 해당 프로젝트를 로컬저장소에 가져옴</br></br>

```bash
$git branch branch_name
```

-   지정한 브랜치 이름을 가진 새로운 브랜치 생성하는 명령어</br></br>

##### 브랜치 생성하는 이유?

1. 협업 시 발생하는 문제 -> 같은이름.같은확장자 인 파일을 의도치 않게 만들게 되면 처음 추가한 이후로는 다시 추가할 수 없다. </br>

2. 여러 기능을 가진 프로젝트를 진행할 시 이전에 개발하였던 기능에 문제가 발생하게 되면</br>현재까지 진행하였던 커밋 내역 전체를 삭제해야되는 문제가 발생.</br></br>

```bash
$git checkout branch_name
```

-   checkout을 통해 브랜치 전환</br></br>
