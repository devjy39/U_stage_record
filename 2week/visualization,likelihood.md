#### matplotlib

    fig = plt.figure()
    fig.set_size_inches(10, 10)  # 싸이즈 설정
    # plt.style.use("ggplot")    # 스타일적용

    ax = []
    colors = ["b", "g", "r", "c", "m", "y", "k"]
    for i in range(1, 7):
        ax.append(fig.add_subplot(2, 3, i))  # 두개의 plot 생성
        X_1 = np.arange(50)
        Y_1 = np.random.rand(50)
        c = colors[np.random.randint(1, len(colors))]

        ax[i - 1].plot(X_1, Y_1, c=c)
<img src=subplot.png>
<img src=explot.png>

#### scatter
    data_1 = np.random.rand(512, 2)
    data_2 = np.random.rand(512, 2)
    plt.scatter(data_1[:, 0], data_1[:, 1], c="b", marker="x")
    plt.scatter(data_2[:, 0], data_2[:, 1], c="r", marker="o")

    plt.show()
<img src=scatter.png>

#### bar chart

    data = [[5.0, 25.0, 50.0, 20.0], [4.0, 23.0, 51.0, 17], [6.0, 22.0, 52.0, 19]]

    X = np.arange(0, 8, 2)
    plt.bar(X + 0.00, data[0], color="b", width=0.50)
    plt.bar(X + 0.50, data[1], color="g", width=0.50)
    plt.bar(X + 1.0, data[2], color="r", width=0.50)
    plt.xticks(X + 0.50, ("A", "B", "C", "D"))
    plt.show()
<img src=barc.png>

#### seaborn

#### scatter에 따른 선 그래프를 보여줌
        sns.regplot(x="total_bill", y="tip", data=tips)
 <img src=regplot.png>
 
### hue키워드! hue="column" hue기준으로 데이터를 나눠서 보여준다.
        sns.countplot(x="smoker", hue="time", data=tips)
<img src=hue.png>

#### 통계적모델링
- 적절한 가정 위에서 확률분포를 추정하는 것
- 예측모형은 데이터와 추정방법의 불확실성을고려해 위험을 최소화하는것으로 충분하다

#### 모수적방법론
- 모수: 평균과 분산
- 모수로 확률분포를 추정하는 것
- 확률분포를 가정하지 않고 데이터에 따라 구조나 모수 개수가 유동적이면 비모수방법론이다.
- 확률분포는 가정하는방법들...
- 데이터의 생성원리를 먼저 고려하는것이 원칙이다
- 반드시 모수를 추정한 후에 검정해야한다.

#### 표집분포
- 통계량(표본평균,표본분산)의 확률분포 
- 표본평균의 확률분포는 n이커질수록 정규분포를 따른다.
- 중심극한점 : 데이터가 많으면 많을수록 하나의 값에 몰린다.

#### 최대가능도 추정법 MLE(MaximumLikelihoodEstimation)
- 가능도함수는 모수세타를 따르는 분포가 x를 관찰할 가능성,,  크고작음의 대소비교는 되지만 확률로 해석하면 안 된다.
<img src=mle.PNG>

#### 로그가능도
- 데이터의 숫자가 수억단위가 되면 정확히 계산이 불가능한데,
- 로그를 사용하면 가능도의 곱셈을 덧셈으로 바꿀 수 있기때문에 연산이 가능해진다.
- 연산량을 O(n^2)에서 O(n)으로 줄일 수 있다.
- 대게 손실함수는 경사하강법을 사용하기때문에 음의 로그가능도를 최적화한다.

#### MLE는 불편추정량을 보장하진 않는다.
- 표본의 분산을 구할 때는 n이 아닌 n-1로 나눈다.
- 불편추정량 : 기댓값이 모수와 동일한 추정량.
- 표본평균이 정해졌을 때, x1~xn중에 n-1개가 정해지면 나머지 하나는 종석적으로 정해진다.
- 따라서 표본분산을 구할 때 자유도는 n-1이 되고 표본분산을 불편추정량으로 만들기 위해 n-1로 나눈다.

#### 손실함수들은 확률분포와 데이터에서 관찰되는 확률분포의 거리를 통해 유도한다.

#### 쿨백-라이블러 발산
- 두 확률분포 사이의 거리를 계산하는 함수 중 하나
- 최대가능도에서 로그추정법에서 최대화시키는것과 정답레이블P와 모델예측Q의 거리를 최소화 하는것과 동일하다.
- 결국 기계학습의 원리는 데이터로부터 확률분포사이의 거리를 최소화하는 것과 동일한 것이다.
<img src=kl.PNG>
