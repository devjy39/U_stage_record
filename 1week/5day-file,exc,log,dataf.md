### python Exception!

    try: except: else: finally:

#### 필요에따라강제로Exception을발생
    raise Exception
#### 특정조건에만족하지않을경우예외발생
    assert f(a, b)
    

    
### FILE 파일 처리

    f = open("<파일이름>" , "접근 모드")
    f.close()

#### r read-읽기모드 - 파일을 읽기만 할 때 사용
#### w write-쓰기모드 - 파일에 내용을 쓸 때 사용
#### a append-추가모드 - 파일의 마지막에 새로운 내용을 추가 시킬 때 사용

### with구문이 끝나게되면 자동 File.close()됨!
    with open("i_have_a_dream.txt" ,  "r") as my_file:
      contents = my_file.read()
      print (type(contents), contents)
      

### WRITE  window는 cp949 그 외 utf8
    with open("count_log.txt", 'a', encoding="utf8") as f:
      for i in range(1, 11):
      data = "%d번째 줄입니다.\n" % i
      f.write(data)

#### pathlib 모듈! path를 객체로 사용가능
    import pathlib

    cwd = pathlib.Path.cwd()
cwd
    WindowsPath('D:/workspace')
cwd.parent
    WindowsPath('D:/')
    list(cwd.parents)


### PICKLE  쓰는 pickle.dump와 읽어오는 pickle.load
    import pickle
    f = open("list.pickle", "wb")
    test = [1, 2, 3, 4, 5]
    pickle.dump(test, f)

    f = open("list.pickle", "rb")
    test_pickle = pickle.load(f)
    print(test_pickle)
    f.close()

### logging ! log의 Level DEBUG > INFO > WARNING > ERROR > Critical

    import logging
    logger = logging.getLogger("main")
    stream_hander = logging.StreamHandler()
    logger.addHandler(stream_hander)
    
#### 기본 warning으로 되어있는 level을 조정!
    logger.setLevel(logging.DEBUG)
    
    logger.debug("틀렸잖아!")
    logger.info("확인해")
    logger.warning("조심해!")
    logger.error("에러났어!!!")
    logger.critical("망했다...")















