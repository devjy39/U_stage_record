### 베이즈정리
- 조건부확률을 이용해 정보를 갱신하는 방법
<img src=image/bayes.PNG>

발병률 10%인 A병이 있다.
병에 걸렸을때 검진이 될 확률99% 
걸리지 않았는데, 검진될 확률 확률 1% <br/>
Q)만약 질병에 걸렸다고 검진되었을 때, 실제 질병에 걸렸을 확률?

발병률 P(A) = 0.1 사전확률

걸렸는데 검진 확률 P(D|A) = 0.99 <br/>
걸리지 않았는데 오검진 확률 P(D|ㄴA) = 0.01<br/>
제대로 검사될 확률 P(D) = 0.99 X 0.1 + 0.01 X 0.9 = 0.108<br/>

∴ P(A|D) = 0.1 X 0.99/0.108 ~= 0.916<br/>

만약 걸리지 않았는데, 검진될 확률 확률을 10%로 바꾸면<br/>
P(A|D) =  ~= 0.524 까지 감소한다. (오탐율(Falsealarm)이 오르면 테스트의 정밀도(Precision)가 떨어진다)<br/>

#### 베이즈 정리를 통한 정보의 갱신
- 새 데이터가 들어왔을 때 앞서 계산한 사후확률을 사전확률로 사용하여 사후확률을 갱신할 수 있다.

Q)앞서 A질병의 검진을 받은 사람이 두 번째 검진을 받았을 때 진짜 A질병에 걸렸을 확률은?

갱신된 사후확률<br/>
P(D') = 0.99 X 0.524 + 0.1 X 0.476 = 0.566<br/>
∴ P(A|D') = 0.524 X 0.99/0.566 ~= 0.917

Q)앞서 검진을 두 번 받은 사람이 또 검진을 받고 진짜 A질병에 걸렸을 확률?

갱신된 사후확률 P(D'') = 0.99 X 0.917 + 0.01 X 0.083 =  0.909<br/>
∴ P(A|D'') = 0.917 X 0.99 / 0.909 = 0.998

#### 인가관계
- 조건부확률은 유용하지만 인과관계를 함부로 추론하면 안 된다.
- 인가관계 기반 예측모형은 높은 정확도를 담보하기 어렵지만 데이터분포의 변화에 강건하다.
- 인과관계를 알아내기 위해서는 중첩요인(confoundingfactor)의 효과를 제거하고 원인에 해당하는 변수만의 인과관계를 계산해야한다.

### Deepleaning의 구성요소
- data : model을 learn시킬 data
- model : data를 transform시킬 방법
- loss function : 모델의 정확성을 평가
- algorithm : loss를 최소화 하는 파라미터를 어떻게 조정할 것인가.

#### Beyond Linear Neural Networks
<img src=image/nonlinear.PNG>
weight를 계산할 때 항상 hidden layer에 Nonlinear transform이 필요함을 잊지 말자.<br/>

#### Activationfunctions,  Nonlinear transform 해주는 함수들
<img src=image/nonf.PNG>

#### Multi-Layer Perceptron
- MSE는 항상 도움이 되지 않을 수도 있다. 
- 큰 target data에 에러가 있을 때 그 데이터를 맞추려다 nn가 전반적으로 망가질 수 있다.
- 크로스엔트로피 Loss가 분류문제를 푸는데 최적인가?
<img src=image/loss.PNG>
결국 다양한 상황에 맞는 loss function이 있고 이유를 찾아야한다.

#### Pytorch
- keras와 tensorflow는 지금은 합쳐졌다. - google
- facebook의 pytorch (tensor객체, 자동미분, 다양한 ML함수와 모델!)

#### tensor객체 생성
    t_array = torch.FloatTensor(n_array)

    print(t_array.shape)
    print(t_array.ndim)   
    print(t_array.size())  #사이즈
    t_array[:2, :3]       #슬라이싱
    print(t1.matmul(t2)) #곱
numpy에서 쓰이는 함수들을 대부분 지원해준다.

#### reshape과 같은 기능 함수
    t1.view(-1, 2)

#### #matrix 줄이고, 늘리기
    t1.view(-1, 10).squeeze() #줄이기
    t1.view(-1, 10).squeeze().unsqueeze(dim=0) #늘리기
    
#### argmax :가장 큰 값 인덱스를 나타내게 변환
    y.argmax(dim=1)

### 미분  scala 값 2 requires_grad = 미분을 할건지 지정
    w = torch.tensor(2.0, requires_grad=True) 
    y = w**2
    z = 2*y + 5

#### 미분
    z.backward()

#### 미분 값
    w.grad

#### a = torch.tensor([2., 3.], requires_grad=True) #matrix형태의 값도 넣을 수 있다.

#### optimizer.zero_grad()
- Clear gradient buffers because we don't want any gradient from previous epoch to carry forward, dont want - to cummulate gradients
- 항상 적어줘야 연산이 쌓이는 것 없이 진행된다.

#### __new__  : class의 초기화

torch를 배우니까 이제 제대로 딥러닝을 시작한 것 같다..~
