1주차 2일째 오늘도 파이썬 문법을 배웠다.


### 고차원 배열의 깊은 복사 방법
    import copy
    var = copy.deepcopy(list)

## 파이썬 포멧팅 원칙 지켜야될 것들★
-함수사이는 2줄씩 띄운다<br/>
-while True: 는 권장되지 않음 *자주 사용하긴 하는데 고쳐야겠음.      switch는 잘 안 쓴다고 하셨다.<br/>
-되도록이면 함수에서 리스트값을 직접 안 바꾸는걸 권장  함수 초반에 temp_list = para_list[:] 하고 시작 하는게 좋다<br/>

## ★★★ 몰랐었는데 파이썬에서는 -5부터 256까지는 메모리에 기본적으로 저장되어있다.
# 그래서 저 범위의 숫자 대입 시 메모리 주소만 넣는 샘
# 그래서 is 비교시 참으로 뜸


### 좋은기능 함수들
# all(boolean_list) -> 리스트의 모든 값을 and연산 

# any(boolean_list) -> or연산

# a is b 에서 is는 주소값을 비교

# 랜덤숫자 생성함수 : random.randint(1,100)

# str.isdigit() 문자열이 디지털인지 확인 함수

# str = r"\n " r""은 문자열의 역슬레시 그대로 인지됨

# str.capitalize() 앞글자만 대문자로


  def spam(eggs):
    eggs.append(1) # 기존 객체의 주소값에 [1] 추가
    eggs = [2, 3] # 새로운 객체 생성
  ham = [0]
  spam(ham)
  print(ham) # [0, 1]

#- 파이썬의 가장 큰 특징 – dynamic typing 
# 처음 함수를 사용하는 사용자가 interface를 알기 어렵다는 단점이 있음
# python 3.5 버전 이후로는 PEP 484에 기반하여 type hints 기능 제공
  def do_function(var_name: var_type) -> return_type:
  pass
  def type_hint_example(name: str) -> str:
  return f"Hello, {name}"

## 규율에 맞는 clean code인지 확인하는법
vscode에서 
 docstring ctrl+shift+p -> docstring

터미널에서
  flake8 **.py 파이썬 소스가 pep8 like에 맞는지 확인

  black **.py 알아서 소스를 pep8 like 수준에 맞게 고쳐줌

#PEP최신문서에 의한 포메팅방법
-f"var : {var}" 을 주로사용
-ex)) print(f'{"hi":*>20} !#$ {0.99555:.2f}')


# 깃 에러
   ! [rejected]        main -> main (fetch first)
  error: failed to push some refs to 'https://github.com/TEAMLAB-Lecture/text-processing-jaeyeolso.git'
  git pull origin main 
깃에서 에러가 났는데 정지훈님이 해결해주셨다.




#과제 테스트케이스 실행할 때

  if __name__ == "__main__": 
      unittest.main()
    
  or 

  python -m unittest


## 2일차.. 아직 할만하다.
