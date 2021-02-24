# MYSQL, Work bench 셋업

### MySQL이란?

-   데이터베이스의 한 종류로, 여러 데이터를 저장하기 위해 이용하는 저장소(종가, 최고가, 최저가 등)

-   txt, xlsx파일 형식으로 저장하기에는 데이터의 양이 너무 방대하기 때문에 **데이터에 대한 접근을 용이하게 하기 위해 이용**

### Work bench란?

-   mySQL 관리를 UI형태로 쉽게해주는 퉅

### Setup

1. mysql.com접속 -> download메뉴 -> mysql installer 용량 큰 것 선택 (previous version 선택도 가능)

2. installer 실행

3. 거의 모든 것을 default로 실행하면 됨

4. Accounts and Roles 메뉴에서 MySQL root password 입력, AddUser로 유저 네임 + 패스워드 추가

5. Connect to server -> Accounts and Roles에서 Adduser 했던 유저 네임과 패스워드 입력 후 Check하면 status에 connection succeeded로 바뀜! -> 설치 완료되었다는 뜻

6. MySQL command Line Client 들어가서 password입력

7. 다음의 코드 입력하여 설치여부 최종 확인

```sql
mysql> select version();
```

8. 굳이 shell 환경에서 이용하지 않아도 됨. work bench UI 이용하면 됨!

9. MySQL Connection 클릭하여 패스워드 입력 후 접속

-   나의 설치과정에서 발생했던 사소한 오류

    -   본인 랩탑에는 파이썬 3.9X 버전이 설치되어 있었음

    -   mysql 8.23 기준에서는 파이썬3.8 이하 버전을 요했음

    -   파이썬 3.8 추가 설치 후 check
