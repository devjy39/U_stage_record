## GPT-1
- Open AI(일론머스크 창립)에서 나온 모델
- TEXT + Position embedding -> 12 x self attention block 구조
<img src=image/GPT1.png>

## BERT 
-  Pre-training of Deep Bidirectional Transformers 
-  사전학습 사용 -> 문장에 있는 일부 단어를 맞추는 Pre-training 방식

#### Masked Language Model (MLM)
- 문장에서 하이퍼 파라미터인 k%만큼 word를 masking하고 맞추도록 한다.
- 하지만 k만큼 전부 mask로 치환하면 다른 특성을 가진 task를 수행하는데 어려움이 생긴다.
- 그리하여 고안한 방식 ↓ k가 15일 경우 -> 15% of the words to predict
- 15% 중 80%는 mask : went to the store → went to the [MASK]
- 15% 중 10%는 random word -> 난이도 ↑  : went to the store → went to the running
- 15% 중 10%는 keep the same sentence -> 정답 단어와 같은 단어를 넣고 소신 있게 안 바꾸도록 학습 : went to the store → went to the store

#### BERT 요약
1. Model Architecture
– BERT BASE: L = 12, H = 768, A = 12
– BERT LARGE: L = 24, H = 1024, A = 16

2. Input Representation
– WordPiece embeddings (30,000 WordPiece) : word -> subword embedding
– Learned positional embedding
– [CLS] – Classification embedding
– Packed sentence embedding [SEP]
– Segment Embedding : 2문장이 입력으로 들어올 때 문장을 A/B 이런식으로 구분

3. Pre-training Tasks
– Masked LM
– Next Sentence Prediction

### BERT VS GPT2
- training-data size GPT 800M words BERT 2500M words
- BERT [SEP],[CLS] 토큰, sentence A/B embedding 문장 segment 등을 넣어줌
- batch size : BERT – 128,000 words ; GPT – 32,000 words
- Learning Late : GPT : 5e-5 ; BERT : fine tuning LR
<img src=image/BERTvsGPT2.png>

#### sQuAd : 독해와 질문이 있는 데이터 -> 정답 word의 시작과 끝을 예측하도록 학습함
#### sQuAd 2.0 : 질문에 대한 답이 없는 경우를 추가

### BERT를 이용해 다음에 올 문장 맞추기 문제 풀기
<img src=image/squad.png>

### BERT의 결론
<img src=image/bigmodel.png>
 
- BIG Model help a lot
- 모델 사이즈를 키울수록 pretraining을 통한 성능이 더 오를 것이다라는 전망

### GPT-2 
- tansformer layer 증가
- training data = 40GB of text - good quality
- datasets : reddit에서 좋아요3개이상 받은 문서들을 사용함

## GPT-3 : Language Models are Few-Shot Learners
- 파라미터 수 증가  -> 175 billion parameters
- 많은 데이터와 베치사이즈는 3.2M  
- 예시를 주고 패턴을 맞추는 방식사용
<img src=image/fewshot.png>
 
- zero-shot ,one-shot, few-shot -> example 문장의 개수) 를 가지고 뜻 예측

## ALBERT
- 기존의 큰 모델들의 모델사이즈는 줄이고 학습시간도 빠르게 만드는 pre-trained task 제안
-	선형변환 layer를 추가 ->  공통적으로 선형변환하는 matrix 사용 -> 파라미터 수 상당히 줄음
- Self-supervised Learning을 위한 Lite BERT
<img src=image/ALBERT.png>
 
- 차원 변환을 위한 벡터를 추가해서 파라미터 수를 혁신적으로 줄였다.
- EX) V x H 가 [100 x 500] 을 10의 dimension으로 줄인다고 가정하면 [100 x 15 + 15 x 500]만큼의 파라미터가 필요하다
- 결국 50000 -> 9000 으로 감소한다. 

## ELECTRA
- generator -> BERT + discriminator -> ELECTRA  (GAN)
- 토큰 교체를 정확하게 분류하는 인코더를 효율적으로 학습한다.
- GAN에서 영감을 얻어 모델을 학습해 실제와 가짜 입력 데이터를 구별 함
<img src=image/ELECTRA.png>

## Light-weight Models
- 기존의 Pre-trained 모델들을 경량화 하기 시작.
- DistillBERT (NeurIPS 2019 Workshop) -> teacher 모델과 student 모델을 구현.
- TinyBERT (Findings of EMNLP 2020) -> teacher 모델과 student 모델 hidden state vector에도 적용함.

