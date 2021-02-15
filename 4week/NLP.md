## NLP
- 컴퓨터가 주어진 단어나 문장을 이해하는 NLU와 자연어를 생성하는 NLG task로 구성.
- Language modeling
- Machine translation
- Question answering
- Document classification
- Text mining
- Information retrieval

#### Transformer
- "attension is all you need"
- self attension사용
- 현재 대부분의 자연어처리 딥러닝 모델의 기본이 되었다.

### Word Embedding
- 자연어가 단어들을 특정한 차원으로 이루어진 한 점의 좌표를 나타내는 벡터로 나타내는 기술

#### Word2Vec 
- Word Embedding으로 학습하는 방법 중 가장 유명한 방법
- 비슷한 의미의 단어가 비슷한 좌표로 나타내게 함. 
<img src=image/bayes.PNG>
 
- softmax에서 나온 확률분포와 원본 데이터의 이상적인 확률분포(100%)를 줄이는 softmax Loss function을 사용한다.
- `continuous bag of words CBOW` : 주변단어들을 통해서 중심단어를 예측
- `skip-gram`: 중심단어를 보고 주변단어들을 예측
- https://ronxin.github.io/wevi/ 동작과정을 자세하게 볼 수 있는 사이트

#### GloVe
- Word Embedding으로 학습하는 유명한 방법
- Word2Vec과 차이 
    - 각 입력 및 출력 단어쌍에 대하여 학습데이터 상에서 두 단어가 한 윈도우내 등장 횟수를 사전에 미리 계산.
    - 수식 -> 입,출력 워드의 내적값을  계산값의 log를 취해 두 값이 가까워지도록 하는  Loss function을 사용했다.
 <img src=image/glove.PNG>
  
- 학습결과 man과 woman의 word embedding
 <img src=image/manwoman.png>
 
### Bag of Words
- 딥러닝 기술이 적용되기 이전에 많이 활용되던 단어를 숫자형태로 나타내는 가장 간단한 표현형
- 일명 "단어가방"이라고 불림

1. `Example sentences`: “John really really loves this movie“, “Jane really likes this song”<br/>
    • Vocabulary: {“John“, “really“, “loves“, “this“, “movie“, “Jane“, “likes“, “song”}<br/>
      - 중복 단어를 제외한 word사전화
2. `Vocabulary`: {“John“, “really“, “loves“, “this“, “movie“, “Jane“, “likes“, “song”}<br/>
    • John: [1 0 0 0 0 0 0 0]<br/>
    • really: [0 1 0 0 0 0 0 0]<br/>
    • loves: [0 0 1 0 0 0 0 0]<br/>
    • this: [0 0 0 1 0 0 0 0]<br/>
    • movie: [0 0 0 0 1 0 0 0]<br/>
      - categorical data를 one hot vector로 만든다
3. `Bag of Words Vector`: Sentence 1: “John really really loves this movie“<br/>
    • John + really + really + loves + this + movie: [1 2 1 1 1 0 0 0]
        - 각 one hot vector의 합으로 나타낸다.

#### NaiveBayes Classifier
- Bag of Words를 활용한 대표적인 문서 분류 기법 
<img src=image/bayes.PNG>
<img src=image/naive.PNG>
 
- 최종적으로 계산된 확률값을 비교하여 클래스 분류 예측값을 내놓는다.


