## CNN
### 일반적인(고전적인) CNN의 구조
<img src=image/CNNnet.PNG>
conv layer + pooling layer + fully connected
<br/>
- fully connected는 파라미터가  때문에 없어지는 추세

### stride와 padding
- stride = kennel이 한번에 이동하는 칸 수
- padding = output size를 외부의 0으로 채워서 늘려준다.
<img src=image/padding.PNG>
* input size와 output size를 맞춰줄 때 padding = kernel size // 2 이다.
### parameter의 수
- conv layer의 파라미터 수 : kernel의 크기 x 출력값의 채널 수
- fully connected layer(dense)의 파라미터 수 : input x output
<img src=image/parameterNumber.PNG>

* dense의 파라미터가 압도적으로 많다.
* 그래서 앞단의 conv layer를 늘리고 뒷단의 dense layer를 줄이는 추세다

### AlexNet
- 2개의 GPU로 병렬연산을 위해 병렬 구조로 설계
- ReLU activation 
- Data augmentation, Dropout
<img src=image/alex.PNG>

### VGGNet
- 3by3 kernel만 사용
- 5by5 kernel 과 3by3 kernel 2번 사용하는 것은 같은 outputD가 나오지만
- 파라미터 수는 3by3을 2번 쓰는게 훨씬 적다.
<img src=image/vgg.PNG>

### GoogLeNet
- NIN구조 network-in-network
- 네트워크는 점점 깊어지고 뒷단의 dense layer를 줄이고 앞단에서 1by1 Convolution을 사용해서 파라미터 수를 줄였다.
- deep한 레이어에서 중간중간에 1by1 Convolution을 활용하면 파라미터 수를 줄일 수 있다.
<img src=image/Googlenet.PNG>

#### 1by1 Convolution으로 파라미터를 줄이는 방식
- 채널을 줄인다. 
- layer층을 쌓으면서 파라미터 수를 줄일 수 있다.
<img src=image/1by1c.PNG>

#### ResNet 
- identity map 을 사용해 레이어를 깊게 쌓아도 잘 학습되도록 함 (skip-connection)
<img src=image/bottle.PNG>
- bottleneck : layer 전 후에 1by1 으로 채널을 줄였다가 다시 input channel과 똑같이 맞춰줌
- F(x) + x를 최소화 하기 위해, F(x)를 0에 가깝게 만드는 것이 목적
<img src=image/resnet.PNG>
#### 그 결과 층을 깊게 쌓아도 좋은 성능을 보여주었다.
<img src=image/resnetf.PNG>

#### DenseNet
- denseblock 으로 채널을 늘리고 1by1 conv로 줄이고 반복 
- 간단한 분류에서 많이 쓰인다. concatenation 
<img src=image/dense.PNG>

## Semantic segmentation:
- Fully Convolutional Network를 사용
- 끝에서 fully connected layer를 쓰지 않는다.
<img src=image/convlize.PNG>
#### 그 결과 ooutput에서 heap map으로 classification이 가능해짐
<img src=image/heatmap.PNG>

### YOLO (with Faster R-CNN)
- faster r-cnn : rpn + fast r-cnn
- region proposal net : 특정 바운딩 박스에 물체가 있을 확률을 미리 알고 시작한다.<br/>
YOLO는 네트워크의 최종 출력단에서 경계박스를 위치 찾기와 클래스 분류가 동시에 이루어진다.<br/>
단 하나의 네트워크가 한번에 특징도 추출하고, 경계박스도 만들고, 클래스도 분류하는 것이다.<br/>
<img src=image/yolo.PNG><br/>
좌측의 입력 영상이 네트워크를 통과하면 중앙의 2개의 데이터를 얻는다.<br/>
이안에는 수많은 경계 박스들과 영상을 7x7그리드로 나눴을 때 해당 그리드 셀안에는 어떤 클래스가 있는지에 대한 정보가 있고<br/>
이 중 경계 박스 안쪽에 어떤 오브젝트가 있을 것 같은 확률이 높은 경계박스만 남고 나머지는 제거된다.<br/>
각 그리드 셀은 해당 영역에서 제안한(proposal) 경계 박스안의 오브젝트가 어떤 클래스인지를 컬러로 표현된다.<br/>
그러므로 최종적으로 남은 3개의 경계 박스 안에 어떠한 클래스가 있는지 알 수 있다.<br/>
그래서 우측의 최종 결과를 얻게된다.<br/>
<br/>
요즘은 바운딩박스를 찾는것과 분류를 동시에 진행하는 방식이 추세이다.
