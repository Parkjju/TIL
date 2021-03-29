# 시뮬레이션 변수 설정 함수

-   제공된 simulator.py 실행 뒤에 DB에 저장되는 데이터들은 무엇일까?
-   Datagrip - simulator DB 확인

    1. all_item_db -> 매수 종목 정리
    2. jango_data -> 일별 수익률 정리(누적)
    3. realtime_daily_buy_list -> 종가 등 여러 데이터 반영하여 다음 날 매수할 종목 선정

### 시뮬레이션 파일 분석

-   library - simulator_func_mysql 라이브러리 import

```python
from library.simulator_func_mysql import *
```

-   self.simul_reset 변수 선언

    1. y 입력시 알고리즘 번호에 따라 DB 초기화 한 뒤에 시뮬레이션 진행
    2. n 입력시 알고리즘 번호에 따라 이전 **이전 데이터는 그대로 두고 그 뒤로 이어서 계속해서 시뮬레이션 진행**

-   input_value함수 내에서 simulator_func_mysql 함수에 **알고리즘 번호, DB초기화 여부를 parameter로 넘김**

```python
# simulator_func_mysql.py
class simulator_func_mysql:
    def __init__(self, simul_num, op, db_name):
        self.simul_num = int(simul_num)

        # scraper할 때 start date 가져오기 위해서
        if self.simul_num == -1:
            self.date_setting()

         # option이 reset일 경우 실행
        elif op == 'reset':
            self.op = 'reset'
            self.simul_reset = True
            self.variable_setting()
            self.rotate_date()

        # option이 real일 경우 실행(시뮬레이터와 무관)
        elif op == 'real':
            self.op = 'real'
            self.simul_reset = False
            self.db_name = db_name
            self.variable_setting()

        #  option이 continue 일 경우 실행
        elif op == 'continue':
            self.op = 'continue'
            self.simul_reset = False
            self.variable_setting()
            self.rotate_date()
        else:
            print("simul_num or op 어느 것도 만족 하지 못함 simul_num : %s ,op : %s !!", simul_num, op)

#.....
```

-   variable_setting함수 진입

    1. self.simul_num - 알고리즘 번호 받음. (앞으로 새로운 알고리즘을 개발하여 if연산을 통해 해당 알고리즘 번호를 받아 이용가능)
    2. self.simul_start_date = "시작날짜 설정"
    3. self.db_to_realtime_daily_buy_list_num = 매수 리스트 설정 알고리즘 번호 (**거래량이 많은 주식..**)
    4. self.sell_list_num = 매도 리스트 설정 알고리즘 번호 **(폭락장에서 살아남기)**
    5. 초기 투자자금 (시뮬레이션 초기 투자금액)
    6. 매수 금액 - 한 종목당 투자할 금액
    7. 자산 중 남겨둘 금액
    8. 익절 수익률 기준치 - self.sell_point
    9. 손절 수익률 기준치 - self.losscut_point =-2
