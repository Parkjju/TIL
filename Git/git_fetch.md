# git fetch & pull의 차이점

-   [참고자료 - Gyun's 개발일지 - pull과 fetch의 차이는 무엇일까?](https://devlog-wjdrbs96.tistory.com/236)
-   [DEV유자 - pull과 fetch의 차이](https://yuja-kong.tistory.com/60)

### git fetch란?

-   페치(fetch)란 원격 저장소의 커밋들을 로컬 저장소로 가져온다. - **자동으로 병합(Merge)를 해주지 않기 때문에 직접 확인 후 병합 과정을 거쳐야함.**
-   로컬 브랜치는 그대로, 원격 저장소 origin/main만 가져온 최신 커밋을 가리킨다

```bash
$git diff HEAD origin/main
$git log --decorate --all --oneline
$git merge origin/main
```

1. git diff HEAD origin/main -> 원래 내용과 바뀐 내용과의 차이 확인
2. git log --decorate --all --oneline -> commit이 얼마나 되었는지 확인 (?)
3. 세부 내용 확인 이후 git merge origin/main -> git pull과 상태가 같아짐.

### git pull이란?

-   git pull이란 원격 저장소의 정보를 가져오며 자동으로 로컬 브랜치에 **병합(Merge)까지 수행해주는 명령어**

*   병합 이후 로컬 브랜치와 원격 저장소 origin/main이 같은 위치를 가리킨다
