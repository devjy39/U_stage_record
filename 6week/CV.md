# Computer Vision

## Transfer learning 전이 학습
- CNN 기반의 딥러닝 모델을 제대로 훈련시키려면 많은 수의 데이터가 필요한데, 이러한 현실적 어려움을 해결하는 방법
- 아주 큰 데이터셋에 훈련된 모델의 가중치를 가지고 와서 우리가 해결하고자 하는 과제에 맞게 재보정해서 사용하는 것
<img src=image/TL.PNG>
 
- Fully Connected Layers를 교체.

## Fine-tuning
- 기존의 Convolution Layers는 Low한 Learning rate
- 새로 교체된 Fully Connected Layers는 High한 Learning rate를 적용하여 학습한다.

## Knowledge distillation(증류)
<img src=image/KD.PNG>
 
- 미리 잘 학습된 큰 네트워크(Teacher network) 의 지식을 실제로 사용하고자 하는 작은 네트워크(Student network) 에게 전달하는 것
- 두 네트워크의 분류 결과를 비교하기 위해 `soft label`을 사용.
  - `soft label`: one-hot vector인 hard label 대신, 정보의 손실 없이 network 를 모방 하도록 (0.14, 0.8, 0.06)이러한 확률값을 학습한다.
- Distillation Loss(teacher network의 loss)와 Student Loss(정답 label의 loss)를 동시에 학습.

## Semi-supervised learning
- 정답 데이터를 수집하는 데이터 레이블링 작업에 소요되는 많은 자원과 비용을 해결하기 위한 방법
- unsupervised 와 supervised를 합친 방법이라고 할 수 있음.
<img src=image/semisuper.PNG>
 
1. 레이블링된 데이터셋으로 모델 학습
2. 학습된 모델로 레이블이 없는 데이터셋을 예측
3. 두 데이터셋을 합쳐서 다시 모델 학습

## Self-training
- Augmentation + Teacher-Studentnetworks + semi-supervisedlearning
- 2019년도에 image Net에서 가장 압도적인 성능을 보여준 모델.
<img src=image/selft.PNG>
 
1. 1M의 레이블링된 데이터로 Teacher model 학습.
2. 학습된 모델로 300M의 레이블이 없는 데이터를 예측 -> pseudo-labeled data
3. 두 데이터셋과 RandAugment를 적용한 추가 데이터까지 합친 방대한 데이터셋을 이용해 Student model을 학습.
4. Teacher Model <- Student Model  : Teacher Model을 없애고 Student model로 대체
5. 더 크고 새로운 Student Model 생성 후 3번처럼 학습. -> Knowledge distillation과 반대로 student model이 점점 커지게 된다.
6. 위 과정 반복 

