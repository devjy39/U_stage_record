## optimization 최적화
#### Generalization
- 제한적인 데이터를 계속 학습시키다보면 testdata에 대한 error가 높아지는데, 이러한 경우 일반화성능이 떨어진다고 표현한다.

#### Under-fittingvs.over-fitting
- underfitting : 모델이 너무 간단하기 때문에 학습 오류가 줄어들지 않는 것.
- overfitting : 학습데이터에서는 잘 되지만 테스트데이터에서는 잘 맞지 않음.

#### Cross-validation
- 학습데이터를 나눠서 일부분은 남기고 validation에 사용한다.
<img src=image/crossv.PNG>

#### Bias-variancetradeoff
- 탄착군을 생각하면 좋다.
- vias를 낮추게되면 variance가 높아질 가능성이 크고
- variance를 많이 낮추면 vias가 높아진다.
<img src=image/viasvar.PNG>

#### Bootstrapping
- 랜덤 샘플링을 통해 training data를 늘리는 방법이다.
- Bagging : 학습데이터를 여러개를 만들고 여러 모델을 만들어서 독립적으로 output을 평균을 낸다. 
- 캐글에서 주로 사용하는 앙상블.
- boosting : 여러개의 모델을 만들어서 sequential하게 합친다.
<img src=image/bootstrap.PNG>

## Gradient Descent Methods 경사하강법 
- stochastic Gradient Descent: single sample만으로 업데이트
- mini-batch Gradient Descent: batchsize만큼 활용해서 업데이트
- batch      Gradient Descent: 한번에 다 사용하여 업데이트

#### batch-size 
- 사이즈가 크면 sharp minimizer
- sharp minimum : training data에서만 좋아짐 일반화성능이 안 좋아짐
- 작으면 flat minimizer 
- flat minimum : training data와 testdata의 성능차이가 비슷해진다. 일반화성능이 좋아짐
- 결국 적절한 leaning rate값을 찾는게 너무 중요하다.

### Optimization
<img src=image/optbasic.PNG>
일반적인 경우

- Momentum
<img src=image/optmom.PNG>
momentum 베타 파라미터가 추가되어 grad와 베타를 합친 accumulation grad로 경사하강법한다.

- nesterov Accelerated Gradient lookahead gradient 
<img src=image/optlook.PNG>
lookahead gradient를 사용해 local minimum을 빠져 나가는데 도움이 됨

- adagrad
lr를 sum of grad로 나눠준다. 
문제점: 나중에 가면 lr가 점점 낮아져 학습이 안 된다.

- adadelta 
adagrad의 문제점을 해결하기 위한 방법

- RMSprop
adagrad에서 stepsize를 추가한 방법

#### Adam
- adaptive와 momentum 방법을 잘 합친 방법
- 가장 성능이 좋고... 좋다고 한다.
<img src=image/adam.PNG>

## regularization 
- 학습데이터 말고 테스트 데이터에서도 잘 돌아가게 하는 방식
- early stopping : test loss가 늘어날때 멈춤
- parameter norm penalty: 함수공간을 부드럽게 보자

결국 데이터가 많아지면 성능도 좋아진다.
#### data augmentation
- 데이터의 각도나 뒤집기 등등 하여 새로운 데이터를 만들어낸다. 
<img src=image/aug.PNG>

#### noise robustness
- 데이터에 노이즈를 넣어서 새 데이터를 만들어낸다.
<img src=image/noise.PNG>

#### label smoothing
- 라벨을 섞거나, 자르고, 특정영역을 합쳐서 새 데이터를 만들어낸다.
- 라벨 평가값이 다양하게 나온다. ex) dog 0.5, cat 0.5
<img src=image/smooth.PNG>

