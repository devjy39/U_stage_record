## Sequence To Sequence
- many to many 구조의 RNN : INPUT : word단위 문장 --> OUTPUT : word단위 문장
- 아무리 LSTM방식을 사용 한다고 한들 멀리있는 word의 정보는 약해진다.
- 그래서 RNN과 Attention을 결합한 `sequence to sequence with Attension`을 사용한다.

## sequence to sequence with Attension
- Encoder -> Decoder -> Attention scores 구조
- encoder를 거치고 나온 Decoder h벡터를 이전 h(1~n)벡터와 내적해서 attention socres에 넣는다.
- 그리고 그 값들을 softmax F으로 확률값을 얻는다. 그럼 encoder hiddenstate vector들에게 가중치를 부여할 수 있음
- attension output은 가중평균 확률값 으로 context vector라고도불림
- input은 decoder h와 encoder h(1~n)
- 그리고 attension output과 decoder h를 input하면 다음 단어 예측값 y가 output
- 예측값 y와 decoder h1을 input으로 decoder h2가 나온다.
<img src=image/sts.png>
 
### teacher forcing
- 첫 예측값이 틀리면 다음 예측값부터는 이상한 데이터가 나오기때문에
- 학습 초반엔 `teacher forcing`을 사용하여 학습하고 후반부엔 예측값 넣어주는 식으로 학습하거나
- 정답데이터와 예측데이터를 적절히 나누어서 넣기도 함. 

### attension 모듈
<img src=image/dot.png>
 
1. 내적
2. attension score를 구하는 general 방식 내적연산 중간에 가중치에 해당하는 벡터를 넣어 학습한다. 
3. concat 방식 concat-> wa-> tanh비선형변환 -> v(a)선형변환(다시scala)
- grad vanishing 해결가능

### greedy decoding
- 순차적으로 단어를 생성하기 때문에 잘못된 단어가 생성 됐다고 알아차려도 해결하기위해 모든 경우의 수를 계산하는 것은 너무 많은 연산이기 때문에 되돌아갈 수 없다.

## beam search
- 자연어 생성 모델 중 test time이 좋은 모델
- beam size (일반적으로 5~10) k개의 경우의 수를 고려한다.
- socore = log버전의 확률값을 더하는 식
- 모든 경우의 수를 다 고려하는 것은 아니지만 훨씬 효율적
- <img src=image/beamscore.PNG>

#### - ex) k= 2인 beam search
<img src=image/beam.PNG>
1. 예측값이 높은 2개의 word를 뽑는다.
2. log를 취한 확률값은 -를 갖는다. 확률이(0~1)이기때문
3. 그 다음 예측단어와 log확률을 더해서 값이 나옴.
4. k²개의 값 중에 가장 큰 k개의 값을 고르는 식으로 decoding한다.
5. 각 경우의 수는 서로 다른 시점의 END token을 생성할 수 있다.

- 중단시점: 미리정해준 n개의 completed hypotheses가 나올 시 중단.
- 그 중 가장높은 score 선택
<img src=image/average.PNG>
 
- `하지만` 길이가 더 긴 경우는 더 낮은 점수가 나오게 되는데 -> score는 -값이기 때문
- 그래서 단어의 개수로 나누어서 word당 평균점수로 비교하게 된다.

#### 정밀도 `precision` = 맞은 단어 수 / 생성된 문장의 단어 수 - 예측값의 실질 정확도
<br/>
#### 재현율 `recall` = 맞은 단어 수 / 정답 문장의 단어 수 - 빠짐없는 정보를 나타내었는가.
<img src=image/precision.PNG>

- 두 값의 산술평균 -> (p1 * p2) / 2
- 기하평균 -> (p1 * p2)½
- 조화평균 -> 1 / {( 1/p1 + 1/p2 ) / 2 } 
- 값이 큰 순서 `산술 > 기하 > 조화`

####F-measure
- 조화평균 -> 작은 값에 더 치중
- 하지만 단어는 다 맞았지만 순서는 엉망인 경우 확률이 100%가 나오는 문제가 생긴다.
<img src=image/fmeasure.PNG>

## BLEU score
<img src=image/bleu.PNG>
 
- Ngram : N개의 연속된 단어가 얼마나 겹치는가
- precision만을 고려 (1~4)gram 단위로 기하평균 (p1 * p2)½ 사용
- `brevity penalty` : 길이만을 고려했을 때 길이가 더 짧으면 precision값을 짧아진 비율값으로 낮춰주고
- 길어지면 최대값인 1이나옴 recall도 어느정도 고려한 방법.
