# 데이터베이스 연동하기

-   mysql 데이터베이스와 pythoon 프로그램을 연결하기위한 패키지 코드

-   해당 패키지를 설치해야함

-   [파이썬 패키지 설치 코드 참조](https://github.com/Parkjju/TIL/blob/master/Python/newbie/modules.md)

```python
from sqlalchemy import create_engine
import pymysql

pymysql.install_as_MySQLdb()
```

-   collector.py -> 파이참 프로젝트에 깔린거 참조

### 수정해야 할 것들

1. Access denied -> 로그인 시 필요한 정보에 대해 잘못 입력 -> 아이디, 패스워드 값 수정

2. db_name -> 조회할 데이터베이스 이름

3. db_id -> mysql 아이디

4. db_passwd -> mysql 접속시 입력했던 패스워드

5. db_ip -> 자신의 PC에서 데이터베이스 구축 -> localhost

6. db_port -> default로 3306포트

### mysql 까먹은 아이디 조회하기

-   MySQL Command Line Client 들어가기

```sql
mysql> select user, host from user;
```

-   위 코드 입력시 여러 유저 등장함
