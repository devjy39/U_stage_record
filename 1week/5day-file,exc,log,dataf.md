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

### configparser    cfg파일 다룰때! 사용

        import configparser
        config = configparser.ConfigParser()
        config.sections()
        config.read('yolov3-tiny.cfg')
        config.sections()
        for s in config.sections():
            print(config[s])
            for key in config[s]:
                print(f"{key} : {config[s][key]}")
            print()
####  출력
        <Section: net>
        batch : 64
        subdivisions : 16
        width : 416
        height : 416
        channels : 3
        momentum : 0.9
        decay : 0.0005
        angle : 0
        saturation : 1.5
        exposure : 1.5
        hue : .1
        learning_rate : 0.001
        burn_in : 1000
        max_batches : 10000
        policy : steps
        steps : 8000,9000
        scales : .1,.1

        <Section: maxpool>
        size : 2
        stride : 2

### argparser 파일 실행 때 옵션 -a -b 
        parser = argparse.ArgumentParser(description='Sum two integers.')
        parser.add_argument('-a', "--a_value", dest=”A_value", help="A integers", type=int)
        parser.add_argument('-b', "--b_value", dest=”B_value", help="B integers", type=int)
        
#### Log의 결과값의 format을 지정해줄 수 있음
        formatter = logging.Formatter('%(asctime)s %(levelname)s %(process)d %(message)s')
        
#### 출력 2018-01-18 22:47:04,385 ERROR 4410 ERROR occurred

### Comma Separate Value csv파일 XML, json, 웹크롤링, 정규식은 다뤄봐야 감이오니 주말에 개인실습을 진행해야 겠다..!





