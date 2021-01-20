## 자료구조와 pythonic code

#### set = {}  의 연산

  a | b = a.union(b)  합집합

  a & b = a.intersection(b) 교집합

  a - b = a.difference(b) 차집합


### collections 

    def general_list(): <br/>
        just_list = []<br/>
        for i in range(100):<br/>
            for j in range(100):<br/>
                just_list.append(i)<br/>
                just_list.pop()<br/>
    %timeit general_list()<br/>
  
  실행결과 : 2.41 ms ± 5.89 µs per loop (mean ± std. dev. of 7 runs, 100 loops each)<br/>

    from collections import deque<br/>
    def deque_list():<br/>
        deque_list = deque()<br/>
        for i in range(100):<br/>
            for j in range(100):<br/>
                deque_list.append(i)<br/>
                deque_list.pop()<br/>
    %timeit deque_list()<br/>

  실행결과 : 683 µs ± 6.48 µs per loop (mean ± std. dev. of 7 runs, 1000 loops each)<br/>
-deque와 list 속도 차이;; 3배 이상 난다.<br/>
-보다시피 같은 연산인데도 차이가 많이 난다. 
<br/><br/><br/>

    from collections import defaultdict
    dd = defaultdict(lambda : 0)
### defaultdict 기본 0으로 설정하면 dict와 달리 없는키에 += 1 해줘도 에러가 안난다.

    from collections import Counter
    c = Counter('helloworld')
### Counter({'h': 1, 'e': 1, 'l': 3, 'o': 2, 'w': 1, 'r': 1, 'd': 1}) 말그대로 세주는 함수 단어세기에 좋음

### *import pprint  #밑으로출력 해주는 pprint.pprint()


## pythonic code
-파이썬 권장 규칙같은 것이다 보기도 좋고 효율도 좋으니 쓰는게 좋다.
 
### list comprehension 리스트 만들때 편하다. 속도도 더 빠르다.
    l2 = [i if i%2==0 else -1 for i in range(10)] 
    [[w.upper(), w.lower(), len(w)] for w in words] 응용

#### dict comprehension 응용
    { v : i for i, v in enumerate(words)} 
  
#### zip함수 두 list를 묶어서 하나씩 출력해주는 함수
    list(enumerate(zip(l1,l2)))
    [(0, ('a', 'w')), (1, ('b', 'x')), (2, ('c', 'y')), (3, ('e', 'z'))]
  
##### lambda,map,.reduce은 권장하지 않는 추세 그러나 많이 씀

### 제네레이터함수 메모리와 시간절약 가능
    def generator_list(value):
        result = []
        for i in range(value):
            print(i)
            yield i

    if 7 in generator_list(30):
        print("fine seven")
    #print(generator_list(50))
    sys.getsizeof(generator_list(50))

#### 함수 밖에서 함수 안의 반복문에 접근(?)이 될 수 있다. 상당히 효율

### 제네레이터 만드는법 * 큰 데이터, 파일데이터, 루프중간에 break 시 주로 사용
    gen_ex = (n**2 for n in range(100)) 
  
### 튜플형태로 들어가는 가변인자 asterisk   *args    => tuple type으로 들어가는 가변인자들
### **은 dict타입으로 들어감                **kwards => dict type일 경우

    def kwargs_test_3(one,two,*args,**kwargs): 
        print(one+two+sum(args))
        print(kwargs)                    

    kwargs_test_3(3,4,    5,6,7,8,9,    first=3, second=4, third=5)

#### unpacking 효과
    print(*["1","2","3"])
    1 2 3
  
  
#### 오늘 중요한 내용이  많았어서 좋았다.
