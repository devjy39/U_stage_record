## RNN
- 바닐라(vanilla RNN)는 아무 것도 첨가하지 않은 처음 상태의 아이스크림을 의미한다.

### RNN의 구조
- one to one -stand nn
- one to many - rnn구조에서 추가 입력이 없는경우는 같은차원의 모두 0으로채워진 벡터를 입력으로 주게된다.
- many to one - sequence text-> 긍,부정
- many to many - machine translation 번역
- many to many - 실시간성 입력데이터구조
<img src=image/RNNtype.png>

### Character-level Language Model
- Example ) sequence “hello”의 학습방법
- Vocabulary: [h, e, l, o]

<img src=image/hello.png>
 
- hello의 input data
<img src=image/hellooutput.png>
 
- 선형변환을 거치고 output vector를 classification을 하기 위해 softmax layer에 input하면 가장 큰 값을 가지는 vector가 큰 확률이 된다.
- 때문에 초록색 정답 데이터의 수치를 높히는 방향으로 학습한다.

### BPTT- Backpropagation through time
- 긴 길이의 Seqence 문장을 truncate로 나누어서 gpu에 학습을 돌릴 수 있다.
- 보통 전체 시퀀스(문장)를 하나의 학습 데이터(샘플)로 생각하고, 총 에러는 매 시간(truncate) 스텝(단어)마다의 에러의 총 합으로 취한다.

## LSTM
- RNN의 backpropagation은 w가 1보다 작으면 h값이 기하급수적으로 0에 가까워지기 때문에 멀리있는 정보가 미미해 지는데 그를 보완한 방법
- i: Input gate, Whether to write to cell
- f: Forget gate, Whether to erase cell
- o: Output gate, How much to reveal cell
- g: Gate gate, How much to write to cell
<img src=image/LSTM.png>

## GRU
- LSTM의 모델구조를 경량화해서 적은메모리 요구량과 빠른 계산 시간
- cell state vector와 hidden state vector를 일원화해서 오직 hidden state vector만 있음
<img src=image/gru.PNG>
 
- forget gate 대신에 1-inputgate의 값을 사용했다.
- h(t-1)과 h(t)간의 가중평균 형태의 계산이 이루어진다.
- 그럼에도 LSTM에 비해 뒤지지 않는 성능을 보여준다.

#### 필요한 정보를 곱셈이 아닌 덧셈을 사용하기 때문에 LSTM과 GRU은
#### `gradients explode or vanish`문제를 없앨 수 있다.
- `gradients explode or vanish`란 ?
- grad를 전부 곱해주는 vanilla RNN에서 h값이 1보다 작으면(sigmoid) 0으로 소실되고 1보다 크면(relu) 너무 커져서
- 시퀀스 데이터 길이가 길어지면 불안정해지는 현상
