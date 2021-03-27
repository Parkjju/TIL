# 일별 금융 데이터 콜렉팅

-   [wikidocs 참조](https://wikidocs.net/85333) -> Data 각 테이블이 의미하는 바에 대해 찾아보기.

-   210327 기준 실습 과정 정리

1. daily_craw DB 생성을 위해 collector_v3.py 실행

    - 키움증권 open api 서버 유지를 위해 데이터 조회에 대한 제약
    - 한 번에 999개의 데이터까지만 조회하도록 제약이 걸려있음. (이 외에 다른 제약들 다수)
    - cf.py (mysql연동 및 키움증권 open api 기본설정을 위한 설정파일) 내에 max_api_call 함수가 정의되어있음

2. jackbot1_imi1 - setting_data 테이블의 **daily_crawler 컬럼** -> collector가 daily_craw DB에 2,000여개 모든 종목의 **데이터 수집 완료한 시점의 날짜가 들어옴.**

    - 챕터 7에서 배치파일 설정할때까지는 collector 실행하는 당일 날짜로 변경해두어야함.
    - **중요** - SQL 데이터 수정 후에는 DB라고 써져있는 초록색 버튼을 클릭하여 수정완료 해야함.

3. 이후 수정된 setting_data의 daily_crawler 컬럼 날짜를 수정한 뒤에 collector를 재시작하면, 2000여개 되는 모든 종목을 컬렉팅 완료하였다고 인식하여 다음 작업을 진행하게 된다.

4. daily_buy_list 생성 작업인데, 현재로서는 배치파일이 없는 시점 (봇을 제대로 돌리지 않는 상황) 이기 때문에 적당한 데이터 생성 뒤에 강제종료한다.

5. setting_data 테이블의 daily_buy_list 칼럼 값을 금일 날짜로 수정한다.

6. 분별데이터 수집을 위해 collector를 다시 실행한다.
