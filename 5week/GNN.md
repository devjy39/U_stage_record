# 그래프 신경망 GNN 

##  그래프 신경망의 구조
- INPUT 값: 그래프와 정점의 속성 정보
- 이웃 정점들의 정보를 집계하는 과정을 반복하여 임베딩
- 각 집계 단계를 층(Layer)이라고 부르고, 각 층마다 임베딩
<img src=image/layer.PNG>

### 집계 함수
- 서로 다른 대상 정점간에도 층 별 집계 함수는 공유된다.
- 이웃들 정보의 평균을 계산하고 신경망에 적용하는 역할
<img src=image/share.PNG>

### 수식
<img src=image/totalf.PNG>
 
- 0번째 층에서의 임베딩 hⁿ = 입력 속성 정보
- 마지막 층에서의 임베딩 hⁿ = 출력 임베딩
-『학습 변수(Trainable Parameter) ≒ ( W, B )』는 층 별 신경망의 가중치
- 손실함수 Loss Function
  - 변환식 정점 임베딩에서처럼 그래프에서의 정점간 거리를 “보존”하는 것을 목표
  - 인접성을 기반으로 유사도를 정의한다면
<img src=image/gnnloss.PNG>
 
- 교차 엔트로피(Cross Entropy)를, 전체 프로세스의 손실함수로 사용해서 종단간(End-to-End) 학습

## 그래프 합성곱 신경망(Graph Convolutional Network, GCN)
<img src=image/GCN.PNG>

## GraphSAGE
- 이웃들의 임베딩을 AGG 함수를 이용해 합친(concat)  후
  - AGG 함수로는 평균, 풀링, LSTM 등이 있음.
- 자신의 임베딩과 연결(Concatenation)
<img src=image/SAGE.PNG>

그래프에 합성곱 신경망을 적용하면?
- 이미지에서는 인접 픽셀이 유용한 정보를 담고 있을 가능성이 높지만,
- 그래프의 인접 행렬에서의 인접 원소는 제한된 정보를 가진다.
- 특히 행과 열의 순서는 임의로 결정되는 경우가 많다.

## 기본 그래프 신경망의 한계
- 이웃들의 정보를 동일한 가중치로 평균을 낸다.
- 그래프 합성곱 신경망 역시 단순 연결성을 고려한 가중치이다.

# 그래프 어텐션 신경망(Graph Attention Network, GAT)
- 가중치 자체도 학습한다.
- W와 a는 역전파를 통해 함께 학습하는 변수
- 가중치를 학습하기 위해서 셀프-어텐션(Self-Attention) 사용
<img src=image/attention.PNG>

## 지나친 획일화
- 정점의 임베딩이 서로 유사해지는 현상
- 작은 세상 효과와 관련
- 신경망의 층이 2~3개 일 때 정확도가 가장 높음.






