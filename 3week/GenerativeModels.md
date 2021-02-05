#### Generative Models
- 생성모델
- <strong>Explicit model</strong> : input에 대한 확률값을 얻어낼 수 있는 모델
- <strong>Implicit model</strong> : 단순히 Generation만 하는 모델
- <strong>Autoregresive model</strong> 자기회귀 : 조건부 확률을 이용해 파라미터 수를 2ⁿ에서 2n-1 로 줄이는 방법을 활용하였다.
<img src=image/independence.PNG>

### Variational Auto-encoder
- Auto Encoder
    - 입력을 기반으로 특징을 추출하고 그 특징으로 다시 원본 데이터를 출력하는 네트워크
    - Encoder와 Decoder로 이루어져 있고, 추출된 특징들을 하나의 특정 숫자값으로 갖는다.
    <img src=image/AE.PNG>
- VAE는 AE에서 추출된 특징의 값을 하나의 숫자가 아닌 가우시안 확률 분포에 기반한 확률 값으로 나타낸 것이다.
<img src=image/VAE.PNG>
<br/>
<img src=image/ELBO.PNG>
 
- VAE로 학습하는 `KEY Idea`
    - 타겟 데이터가 없으므로 Objective를 계산할 수 없는데 ELBO를 계산해 키움으로써 Objective를 줄이는 것이다.

## GAN (Generative Adversarial Networks 적대적 생성모델)
- 위조지폐범과 경찰은 한 쪽이 더 잘하면 다른 한 쪽도 더 잘하려고 할 것이기 때문에 결국 위조 지폐는 점점 더 진짜 같아지는 것
<img src=image/theif.PNG>

<strong>minimax game</strong> : 서로 반대되는 목표의 대결
<img src=image/GAN.PNG>
- Discriminator는 objective function을 최대화하는 방향으로 할습할 것이고,
- Generator는 objective function을 최소화하는 방향으로 학습할 것이다.

### DCGAN (Deep Convolution GAN)
- GAN의 Generator를 구성할 때 이미지의 특화된 CNN을 적용한 모델
<img src=image/DCGAN.png>

### CycleGAN
- 서로 다른 도메인으로 데이터를 바꿀 수 있는 모델.
- 서로가 서로의 Generator이자 Discriminator가 되는 방식으로 되어있다.
- Cycle-consistency loss 
    - 기존의 Loss에 추가적으로 Cycle로 인한 Loss까지 추가함.
    - 말(X)를 넣고 얼룩말(Y)가 나오고, 다시 그 얼룩말(Y)로 말(X)이 나오게 해보면, 기존의 말(X)과 어느정도 차이가 생기는데 이를 `Cycle-consistency loss`라고 한다. 이 차이를 최소화 시키는 방향으로 학습한다.
<img src=image/horse.PNG>



`오늘 생각할 것`
-교수님이 CNN모델 파라미터 수를 계산하는 습관을 들이면 네트워크의 규모를 가늠할 수 있어 좋다고 하셨다.
