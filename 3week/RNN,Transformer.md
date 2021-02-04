## RNN
- 시퀀스 데이터: 시계열 데이터, 가변적인 데이터
- 처리 하기 위해선 x1부터 x(t-1)까지 조건부확률을 이용한다.
- 하지만 모든 과거 데이터가 필요하진 않음
- 길이가 가변적인 데이터를 다룰 수 있는 모델이 필요.
- RNN은 잠재변수를 복제해서 다음 시점에 활용한다.
<img src=image/RNN.png>
`RNN의 단점` :Long term dependency 오래된 과거 데이터의 활용이 힘들다.

#### bptt
- h(t+1) 잠재변수와 O(t+1) 출력을 입력과 이전 시점 h(t)잠재변수에 전달된다.

#### truncated BPTT
- grad를 전부 곱해주는 연산이라 1보다 작으면(sigmoid) 0으로 소실되고 1보다 크면(relu) 너무 커져
- 시퀀스 데이터 길이가 길어지면 불안정해진다.
- 그래서 끊는 것이 필요한데 미래 정보 몇 개는 자른다
- 중간에 모든 미래 시점의 잠재변수H(t+1)를 빼고 출력 O(t)에서만 grad를 받아서 H(t)에서 연산한다.

`Fix the past timespan` : 과거 몇 개의 고정 수의 데이터만 보는 것

`latent autoregressive model` : hidden state 과거의 정보를 요약하고 있는 정보

### `LSTM` Long Short Term Memory
- forget gate : 어떤 정보를 버릴지 sigmoid -> 항상 0~1값 ft - 이전까지 들어왔던 정보를 현재 입력을 바탕으로 지울지 
- input gate : 어떤 정보를 올릴지 , ct (-1~+1) cell state 예비군-현재 입력을 바탕으로 어떤 값을 새롭게 쓸지 
- update cell :  it ct 로 어느정보를 올릴지 정함 - 이 두 정보를 취합
- output gate :  이 취합한 cell state를 한번 더 조작해서 어떤 값을 output으로 빼낼지
<img src=image/LSTM.PNG>

### GRU 
- lstm보다 적은 파라미터로 성능이 더 좋은 지만, 요즘은 사용 안 하는 추세
- reset gate 
- update gate 
- no cell state
- only hidden state
<img src=image/GRU.PNG>

## Transformer
- n개의 단어를 한번에 처리할 수 있는 구조
- INPUT -> ENCODER -> DECODER -> OUTPUT
- ENCODER = self-attendtion + feed forward neural network
- self-attendtion : n개의 벡터를 나머지 벡터도 고려해서 n개의 출력이 나옴. 다른 벡터와 관계성을 생각한다.
<img src=image/transf.png>


### Encoder
- 3가지 nn이 있다. queries와 keys벡터는 내적해야되니 항상 차원이 같아야된다
- queries
- keys
- values
- score -> queries와 나머지 n개의 keys벡터를 내적 -> 나머지 단어와 관계
- divide by 8 queries와 keys벡터의 차원의 루트로 나누고 그 값을 softmax한다.
- 최종적으로 output은 value벡터의 weighted sum.
<img src=image/encoder.png>

    scores = Q.matmul(K.transpose(-2,-1)) / np.sqrt(d_K)
    attention = F.softmax(scores,dim=-1)

앞 서 말한 방식대로 encoding 하면 순서에 상관없이 같은 값이 나오게 되는데
`popsitional encoding`을 사용하면 된다.

### Multi-headed attention
- sequential computation 을 줄여 더 많은 부분을 병렬처리가 가능하게 한다.
- 더 많은 단어들 간 dependency를 모델링할 수 있다.
- 하지만 feed-forward layer은 오직 한 개의 행렬만을 input으로 받을 수 있다. 
- 모든 head를 이어 붙여서 하나의 행렬로 만들어버리고, 그다음 하나의 또 다른 weight 행렬인 W0을 곱해서 1개의 output을 낸다.
<img src=image/mlh.png>

<img src=image/decoder.png>
encoder -> decoder 보내는 데이터 = `key, value`

최근에는 Transformer가 자연어 처리 분야 말고도 vision data 처리에도 활용되고 있다.





























