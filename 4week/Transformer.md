## Transformer

### self attention 모듈
- 입력값 x 벡터는 자기 자신 or 주변 벡터와 내적을 수행하고 나온 유사도 -> softmax로 가중평균을 구해서 encoding vector로 구한다.
- 보통 자기 자신과의 내적값이 높게나오게 된다.
<img src=image/qkv.png width=500 height = 400>
 
`Queries vector` :주어진 벡터들 중 어느 벡터를 선별적으로 가져올지 기준이 되는 벡터
`Keys vector`: queries와 내적하는 재료벡터, 어느 벡터가 유사도가 높은지 결정 해주는 역할
`Value vector`: 재료벡터
- `Queries vector`는 1개 `Keys vector`와 `Value vector`는 워드 수 만큼 같은 개수 생성
 
1. `Queries vector`와 `Keys vector` 내적
2. Softmax연산 
3. `Value vector`와 곱해서 가중평균을 구한다.
- 이로써 같은 벡터와 내적을 해도 유연한 유사도를 얻을 수 있음
- Long-Term Dependency 깔끔하게 해결

<img src=image/sqrtd.png>
 
- softmax연산에서 루트d로 나눠주는 이유: Q,K 벡터의 차원이 커지면 분산과 표준편차가 커지는데,
- 분산 혹은 표준편차가 클 수록 Softmax 확률분포가 큰 값에 몰리고 몰리면 BackPropagation에서 grad vanish로 이어진다.
- 하지만 작은 경우는 좀 더 고르게 퍼지게 된다.

## Multihead attention
<img src=image/mulhead.PNG>
 
- 서로 다른 측면의 정보를 병렬적으로 뽑고 concat해서 서로 다른 정보들을 상호 보완적으로 얻는다.
- 그 후 Linear변환으로 차원을 줄여줌
<img src=image/mha.PNG>
 
## Transformer vs RNN
<img src=image/versa.png>
 
<strong>Transformer는 RNN보다</strong>
- 학습처리 속도는 빠르다 -> RNN은 재귀적이라 각 Time Step을 병렬화가 불가능 함.
- 메모리 요구량이 많음 -> 모든 head의 쿼리와 키의 모든 내적값을 저장하고 있어야 하기때문


## Add & Norm 
- `Add` : residual connection 
  - vector를 요소별로 더함
- `Layer Normalization`
  - (vector - 평균) /분산 
  - affine transformation
<img src=image/affine.png>

## Positional Encoding
- 기존 Encoding은 교환법칙이 성립하여 순서를 무시하고 output값이 나오는 문제가 있음.
- 해결책
<img src=image/position.png>
 
- 위치에 따라 구별할 수 있는 벡터 -> sin cos같은 주기함수를 이용
- 지문처럼 고유의 위치가 나온다.

### Learning Rate Scheduler : adam처럼 유동적인 LR을 사용하는 방법<br/>
 
## Decoder의 Multi-Head Attention
<img src=image/decoder.png>
 
- encoder의 Value ,Key vector를 받아서 Decoder의 Query벡터와 Multi-Head Attention연산
- linear(차원 변환) -> Softmax

## Masked Self-Attention
<img src=image/mask.PNG>
 
- attention에서 뒤에서 나오는 단어에 대한 가중치를 0으로 만들고 이후 value벡터와 가중평균을 내는방식

## Transformer Performance
<img src=image/transformer.png>
 
- BLEU Score는 어순이 달라도 같은 의미일 때 낮은 점수를 부여해서 일반적으로 점수대비 성능은 높다.
- EX) 나는 열심히 공부를 한다 =(같은 의미)= 나는 공부를 열심히 한다.

## 결론: Transformer 성능 좋음

