## RNN
- 시퀀스 데이터: 시계열 데이터, 가변적인 데이터
- 처리 하기 위해선 x1부터 x(t-1)까지 조건부확률을 이용한다.
- 하지만 모든 과거 데이터가 필요하진 않음
- 길이가 가변적인 데이터를 다룰 수 있는 모델이 필요.
- RNN은 잠재변수를 복제해서 다음 시점에 활용한다.
<img src=image/RNN.PNG>
- RNN의 단점 Long term dependency 오래된 과거 데이터의 활용이 힘들다.

#### bptt
- h(t+1) 잠재변수와 O(t+1) 출력을 입력과 이전 시점 h(t)잠재변수에 전달된다.

#### truncated BPTT
- grad를 전부 곱해주는 연산이라 1보다 작으면(sigmoid) 0으로 소실되고 1보다 크면(relu) 너무 커져
- 시퀀스 데이터 길이가 길어지면 불안정해진다.
- 그래서 끊는 것이 필요한데 미래 정보 몇 개는 자른다
- 중간에 모든 미래 시점의 잠재변수H(t+1)를 빼고 출력 O(t)에서만 grad를 받아서 H(t)에서 연산한다.

`Fix the past timespan` : 과거 몇 개의 고정 수의 데이터만 보는 것

`latent autoregressive model` : hidden state 과거의 정보를 요약하고 있는 정보


### Long Short Term Memory








































