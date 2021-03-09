## GoogLeNet의 Auxiliary classifier
- googlenet은 1x1 convolution을 사용해 채널 수를 줄여 파라미터를 줄이는 방법을 사용하였다.
- 네트워크 중간중간에 auxiliary classifiers로 grad를 넣어 vanish grad를 해결 함.
<img src=image/Auxiliary.png width=500>
 
- 학습중에 사용하고 테스트할 땐 제거

## resnet
- 2016처음으로 인간레벨의 image net을 넘어서고, 모든 task에서 1등을 했다.
- network의 depth의 중요성을 알려주었다.

## EfficientNet
- scaling 방법을 모두 적절히 사용하여 성능을 높임.
- 압도적인 성능을 보여줬음.
<img src=image/efficientnet.PNG>
 
# Fully Convolutional Networks(FCN)
- 호환성이 높은 구조 -> 기존의 fcl를 Fully conv layer인  1x1conv로 바꾸면 구현가능
- Fullyconnected layer를 Fullyconvolutional layer by 1x1convolutions로 변경
- single feature vector를 convolutional feature map vector수 만큼 늘림

<img src=image/FCN.PNG>
 
- N개의 채널을 m개의 필터 개수만큼 줄임

## upsampling
- pooling으로 줄어든 해상도를 upsampling을 통해 해상도를 증가시킴
- transposed convolution : 중첩되는 픽셀이 CHECK borad처럼 경계선을 무너뜨리는 문제가 생김 - overlap issues
- Nearest-neighbor(NN),Bilinear방법으로 골고루 중첩되게 만듦

# DeepLab

## Dilated convolution
- 파라미터 수는 늘어나지 않고, receptive field를 늘리기 위한 방법
<img src=image/dilated.png>

## Depthwise separable convolution
- 연산량을 줄이기 위해 convoultion 과정을 부분화 함
<img src=image/depthwise.PNG>
 
- 가장 높은 수의 지수가 하나 줄어들어서 연산량 감소
