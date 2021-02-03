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

### parameter의 수
- conv layer의 파라미터 수 : kernel의 크기 x 출력값의 채널 수
- fully connected layer(dense)의 파라미터 수 : input x output
<img src=image/parameterNumber.PNG>

* dense의 파라미터가 압도적으로 많다.
* 그래서 앞단의 conv layer를 늘리고 뒷단의 dense layer를 줄이는 추세다




















