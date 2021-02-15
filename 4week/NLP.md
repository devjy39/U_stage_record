## NLP
- 컴퓨터가 주어진 단어나 문장을 이해하는 NLU와 자연어를 생성하는 NLG task로 구성.
- Language modeling
- Machine translation
- Question answering
- Document classification
- Text mining
- Information retrieval

#### Word Embedding
- 자연어가 단어들을 특정한 차원으로 이루어진 한 점의 좌표를 나타내는 벡터로 나타내는 기술

#### Transformer
- "attension is all you need"
- self attension사용
- 현재 대부분의 자연어처리 딥러닝 모델의 기본이 되었다.

### Bag of Words
- 딥러닝 기술이 적용되기 이전에 많이 활용되던 단어를 숫자형태로 나타내는 가장 간단한 표현형
1. Example sentences: “John really really loves this movie“, “Jane really likes this song”
    • Vocabulary: {“John“, “really“, “loves“, “this“, “movie“, “Jane“, “likes“, “song”}
      - 중복 단어를 제외한 word사전화
2. Vocabulary: {“John“, “really“, “loves“, “this“, “movie“, “Jane“, “likes“, “song”}
    • John: [1 0 0 0 0 0 0 0]
    • really: [0 1 0 0 0 0 0 0]
    • loves: [0 0 1 0 0 0 0 0]
    • this: [0 0 0 1 0 0 0 0]
    • movie: [0 0 0 0 1 0 0 0]
      - categorical data를 one hot vector로 만든다
#### NaiveBayes Classifier
- Bag of Words를 활용한 대표적인 문서 분류 기법 





























