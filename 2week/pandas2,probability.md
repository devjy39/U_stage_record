#### pandas Groupby
    df = pd.DataFrame(ipl_data)
    df.groupby("Team")["Points"].mean()
    
    Team
    Devils    768.000000
    Kings     761.666667
    Riders    762.250000
    Royals    752.500000
    kings     812.000000
    Name: Points, dtype: float64

#### 매트릭스 형태로 반환
    h_index.unstack()

#### date유틸
    import dateutil
    df_phone["date"] = df_phone["date"].apply(dateutil.parser.parse, dayfirst=True)

#### merge
<img src=merge.PNG>
    pd.merge(df_a,df_b, on="_id" how = 'inner' or 'outer' or 'left' or 'right')

#### concat 데이터를 붙이는 연산
    pd.concat([df_a,df_b], axis =  )
    
#### import sqlite3   db라이브러리

### 확률론

#### 이산확률변수 : 확률변수가 가질 수 있는 경우의 수를 모두 고려하여 확률을 더해서 모델링

#### 연속확률변수 : 데이터 공간에 정의된 확률변수의 밀도 위에서의 적분을 통해 모델링
- 밀도는 변화율이지 확률로 해석하면 안된다!

#### 조건부기대값 E[y|x]는 E||y-f(x)||..2 을 최소화하는 함수 fx와 일치한다.

### 몬테카를로 샘플링
- 확률분포를 모를때 데이터를 이용하여 기대값을 대신계산.
- x에 샘플링한 데이터를 넣어주고 x(i)값의 산술평균을 구해주면 기대값과 근사하다.
- 독립적인 샘플링이 필요하다.
- 적분 범위 구간의 길이로 적분값을 나누면 기대값을 계산하는 것과 같은 몬테카를로 방법을 사용할 수 있다.

    import numpy as np

    def mc_int(fun, low, high, sample_size = 100, repeat= 10):
        int_len = np.abs(high- low)  #f(x)함수의 x범위
        stat = []
        for _ in range(repeat):
            x = np.random.uniform(low=low,high=high, size=sample_size) #랜덤x값 생성
            fun_x = fun(x) # 함수에 대입
            int_val = int_len * np.mean(fun_x) #적분값을 2(길이)로나누면 기대값이니 기대값x2는 적분값
            stat.append(int_val)
        return np.mean(stat), np.std(stat) 

    def f_x(x):
        return np.exp(-x**2)

    print(mc_int(f_x,low=-1,high=1))


#### further question
- 몬테카를로 방법을 활용하여 원주율에 대한 근사값을 어떻게 구할 수 있을까.
- x (0~1) y (0~1) 그래프의 너비를 구하고 4배 해주면 반지름1인 원의 너비가 된다. 

    def find_pi(fun, low, high, sample_size = 100000, repeat= 100):
        int_len = np.abs(high-low)
        stat = []
        for _ in range(repeat):
            x = np.random.uniform(low=low,high=high, size=sample_size)
            fun_x = fun(x)
            int_val = int_len * np.mean(fun_x)
            stat.append(int_val)
        return np.mean(stat)*4, np.std(stat)

    def f_x(x):
        return np.sqrt(1-x**2)

    print(find_pi(f_x,low=0,high=1))

출력값 : (3.1415986498727664, 0.0007220831335122185)

값은 잘 나온 것 같다.



















