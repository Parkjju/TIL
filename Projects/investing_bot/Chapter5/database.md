# 시뮬레이터별 자동 데이터베이스 생성 함수

### 시뮬레이터에서 이용하는 변수들 (simulator_func_mysql)

1. self.simul_num = 1 : 알고리즘 번호
2. self.op = 'reset' : option - 이전 시뮬레이터부터 이어갈지 말지 여부 결정
3. self.simul_reset = True
4. self.simul_start_date = "20210402" : 시뮬레이션 데이터 시작일자
5. self.db_to_realtime_daily_buy_list_num = 1 : 매수리스트 설정 알고리즘 번호
6. self.sell_list_num = 1 : 매도리스트 설정 알고리즘 번호
7. self.start_invest_price = 1000000 : 초기자금
8. self.invest_unit = 100000 : 매수 금액
9. self.limit_money = 300000 : 자산 중 최소로 남겨 둘 금액
10. self.sell_point = 10 : 익절 수익률 기준치 (%)
11. self.losscut_point =-2 : 손절 수익률 기준치 (%)
12. self.engine_simulator = simulator1 database에 접속하도록 create engine.
13. self.daily_craw = > daily_craw database에 접속하도록 engine을 만듦
14. create_engine과 관련된 객체들은 각 db에 접속하기위해 객체를 만든다고 생각하면 됨
15. self.db_conn = 특정 데이터베이스가 아닌 mysql에 접속하는 객체이다.

### 시뮬레이터 알고리즘 설정 후 - db_name_setting함수 진입

-   database 세팅함수.

1. self.db_name = "simulator" + str(self.simul_num) .. 시뮬레이터 알고리즘 번호와 함께 시뮬레이터 이름으로 저장.
2. self.engine_simulator = create_engine(..)
    - create_engine - database접속을 위해 engine을 만든 것이다.. (추가 내용 필요)
    - cf mysql 초기설정 파일을 연결하여 cf.id 등 mysql 계정 정보를 전달
