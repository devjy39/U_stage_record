## 이미지 분류 Train data EDA

## 나이, 성별
- 여성이 약 600명정도 더 많음
- 나이 18~ 60세로 중앙값보다 바깥쪽으로 갈 수록 많아짐
<img src=image/eda1.PNG>

 
## 클래스별 데이터
- 60살 데이터 자체는 적은편은 아니지만,
- 나이 분류가 18~ 30, 30~ 60, 60으로 되어있어서 60살의 데이터가 너무 적음 argument가 필요해 보인다.
<img src=image/eda2.PNG>

## dataset
    dataset = []

    for dir in img_list:
        img_dir = [i for i in os.listdir(os.path.join(IMAGE_PATH, dir)) if i[0] != '.']
        sex = dir.split('_')[1]
        age = int(dir.split('_')[3])
        num = -1

        if sex == 'male':
            if age<30:
                num=0
            elif age>=30 and age<60:
                num=1
            else:
                num=2
        else:
            if age<30:
                num=3
            elif age>=30 and age<60:
                num=4
            else:
                num=5

        for i in img_dir:
            if i[:4] == 'mask':
                dataset.append([os.path.join(IMAGE_PATH, dir,i),num])
            elif i[:4] == 'inco':
                dataset.append([os.path.join(IMAGE_PATH, dir,i),num+6])
            else:
                dataset.append([os.path.join(IMAGE_PATH, dir,i),num+12])
    dataset = np.array(dataset)            
    
    len(dataset) = 18900

## sklearn으로 data split
    from sklearn.model_selection import train_test_split

    train_image, test_image, train_target, test_target = train_test_split(dataset[:,0], dataset[:,1], test_size = 0.1 ,stratify=dataset[:,1])
 
- test_size = test비율
- stratify = target -> 클래스별로 비율을 맞춰서 분리해줌 아주 중요한 옵션이다.
- dataset을 만들어 보았다. split 비율을 정해야 하는데 피어세션에서 k-fold방식을 들었다. 추후 적용해야 겠음.
- 모델이 3개가 필요할 것 같았는데, 생각보다 많은 사람들이 같은 생각을 한 것 같음.
- 최신모델 vision transformer가 괜찮다고 한다.
