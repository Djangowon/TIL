# FastAPI Initial Setting
PyCharm으로 처음 프로젝트를 만들면 `main.py` 이 생성된 모습


<img src="https://github.com/Djangowon/TIL/blob/main/image/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-02-14%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%208.35.59.png" height=80% width=80%>
    
    
#### FastAPI 와 uvicorn 을 설치하기
```
$ pip install fastapi
```
```
$ pip install uvicorn[standard] 
```
* uvicorn을 통해 python 서버를 실행시킬 수 있음
* uvicorn을 [standard]로 설치 시 Cython 기반의 디펜던시가 설치된다. 또한, 이벤트 루프인 uvloop가 사용되고 http 프로토콜은 httptools로 처리된다.
* [standard] 생략해도 무방하나, [standrard]로 설치하지 않는 경우 uvloop가 설치되지 않고 대신 event loop로 asyncio를 사용한다. 이 경우에는 성능이 더 떨어지게 됨.

#### 테스트를 위한 main.py 작성
```python
$ vi main.py

from fastapi import FastAPI

app = FastAPI()


@app.get("/")
async def root():
    return {"message": "Hello World"}
```
#### uvicorn runserver 명령어
```
$ uvicorn main:app --reload # 로컬에서 run
$ uvicorn main:app --reload --host=0.0.0.0 --port=8000 # +모든 접근 가능, 포트번호 설정할 때
```
* 뒤쪽에 붙은 --reload 옵션은 hot reloading 기능으로 소스 코드가 수정되면 서버를 바로 재시작하는 기능.

#### 웹 서버를 열어 확인
[http://127.0.0.1:8000/](http://127.0.0.1:8000/)  
```
{"message": "Hello World"}
```
<img src="https://github.com/Djangowon/TIL/blob/main/image/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-02-14%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%208.37.55.png" height=80% width=80%>

Hello World가 잘 출력된다.

#### Swagger를 통해 테스트해보기
[http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs/)  

<img src="https://github.com/Djangowon/TIL/blob/main/image/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-02-14%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%208.39.35.png" height=60% width=60%>

<img src="https://github.com/Djangowon/TIL/blob/main/image/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-02-14%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%208.39.49.png" height=60% width=60%>

Try it out을 누르고 Execute 실행으로 API를 테스트 할 수 있다.  


<img src="https://github.com/Djangowon/TIL/blob/main/image/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-02-14%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%208.40.14.png" height=80% width=80%>


[Ref](https://jybaek.tistory.com/890/)

