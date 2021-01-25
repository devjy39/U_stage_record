#### import numpy as np

### numpy의 array는 c언어의 배열처럼 만들어져 속도가 훨씬 빠르다.

### 기본 array
    arr =[[1,2],[3,4]]
    np.array(arr,dtype = int)
    
    
#### 0~29까지의 array 
    np.arange(30)
    
#### 4by4 0으로 채워진 array
     np.zeros(shape=(4,4),dtype = np.float64)

#### -1은 최댓값이 자동으로 들어간다.  
    np.array(np.arange(30)).reshape(2,3,-1)

#### axis는 축을 말하는데 더 높은차원 축일수록 0부터 추가됨
    mt[np.newaxis,:]


#### empty는 빈배열로 메모리 할당이 이루어지지않음.

#### 균등분포
    np.random.uniform(0,1,6).reshape(2,3)

#### 정규분포
    np.random.normal(0,1,10).reshape(2,5) 

#### 전치행렬 만드는법 2가지
    test_t.T
    test_t.transpose()


#### broad casting이란? 연산 행렬 //*+- 스칼라 연산 지원 
#### 벡터와 연산시 벡터의 크기를 강제로 맞춰줌

#### where a<8 조건에 맞는 불린array에서 true는 5 false는 2할당
    np.where(a<8,5,2)

### 벡터의 노름 norm : 원점에서부터의 거리
    def l1_norm(x):     #robust , raso?
        x_norm = np.abs(x)
        x_norm = np.sum(x_norm)
        return x_norm
    def l2_norm(x):  #라플라스 리치
        x_norm = x*x
        x_norm = np.sum(x_norm)
        x_norm = np.sqrt(x_norm)
        return x_norm

### 벡터간의 각도 구하기
    def angle(x,y):  #inner 내적
        v = np.inner(x,y) / (l2_norm(x) * l2_norm(y))
        theta = np.arccos(v)
        return theta


#### x@y행렬곱 연산자 @


### 역행렬        
#### 역행렬 조건
1.행과 열이 같아야됨 
2.행렬식이 != 0
    np.linalg.inv(x)
    
### 유사역행렬
    np.linalg.pinv(y)

#### 중요한 파트인 NUMPY를 배웠다. 재밌었다.
