### Class의 masic method!
-https://ziwon.github.io/post/python_magic_methods/
-__init__ __str__ __add__ 등등 엄청 많다.'

    class Note(object<상속 함수>):
        def __init__(self, content = None):
            self.content = content

        def del_note(self):
            self.content = ""

        def write(self,content : str):
            self.content = content

        def __add__(self,other : str):
            return self.content + other.content

        def __str(self):
            return self.content


#### self 는 생성된 인스턴스를 가르킨다
    self.__item = private 변수


### get함수 만들때 decorator 숨겨진 변수를 반환하게 해줌 함수명을 변수명처럼 쓰게해줌

    @property  
    def item(self):
      return self.__items
      
#### 보통은 수정을 막기위해 카피해서 return함


### 일급함수
    def square(x):	
    f = square 
    f(5)
-함수를 변수처럼 사용
-수자체를 파라미터로 만들기도 가능


#### inner function 함수안에 함수

### **closures : inner function을 return으로 반환 
    def print_msg(msg):
        def printer():
            print(msg)
        return printer
    another = print_msg("Hello, Python")
    another()

### decorator function

    def star(func):
        def inner(*args, **kwargs):
            print(args[1] * 30)
            func(*args, **kwargs)
            print("*" * 30)
        return inner

    @star
    def printer(msg,g):
        print(msg)
    printer("Hello","^")


### 2중으로 사용한 deco func

    def star(func):
        def inner(*args, **kwargs):
            print("*" * 30)
            print("*" * 30)
            func(*args, **kwargs)
            print("*" * 30)
        return inner

    def percent(func):
        def inner(*args, **kwargs):
            print("%" * 30)
            func(*args, **kwargs)
            print("%" * 30)
        return inner

    @star
    @percent
    def printer(msg):
        print(msg)
    printer("Hello")
    
### @자리에 파라미터를 
    def generate_power(exponent):
        def wrapper(f):
            def inner(*args):
                result = f(*args)
                return exponent**result
            return inner
        return wrapper


    @generate_power(2)
    def raise_two(n):
        return n**2

    print(raise_two(5))

    print(generate_power)


## Python의 Module

#### __pycache__.py  빠른 로딩을 위해 컴파일 해둔 파일

#### m으로 별칭
    Alias)  import module as m   m으로 별칭
    
#### A함수만 호출   *은 ALL
    from module import function_A



