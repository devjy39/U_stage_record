#### pandas as pd
### pandas는 구조화된 데이터를 다루는 라이브러리 python계의 엑셀이라고 불린다.

    data_url = 'https://archive.ics.uci.edu/ml/machine-learning-databases/housing/housing.data' #Data URL
    #data_url = "./housing.data"  # Data URL
    df_data = pd.read_csv(
        data_url, sep="\s+", header=None
    )  # csv 타입 데이터 로드, separate는 빈공간으로 지정하고, Column은 없음

#### Series데이터
- ndarray의 sub class 지만,numpy와 다르게 index가 있음.
    list_data = [i for i in range(10,1,-1)] 
    ex_obj = pd.Series(data = list_data)
    
    0    10
    1     9
    2     8
    3     7
    4     6
    5     5
    6     4
    7     3
    8     2
    dtype: int64

#### df = pd.read_excel("./excel-comp-data.xlsx") 엑셀파일도 열 수 있다..

#### 인덱스를 특정 컬럼으로 변경
    df.index = df["account"]  
#### 특정컬럼 삭제
    del df["account"]    

    df[["name","street"]][:2]

    df.loc[[211829,320563],["name", "street"]]

    df.iloc[:2,:3]
같은 출력방식



























    
    
    
    
    
    
    
    
    
    
    
    
