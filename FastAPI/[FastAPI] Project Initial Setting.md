# Project Initial Setting
PyCharm으로 처음 프로젝트를 만들면 `main.py` 이 생성된 모습


<img src="https://github.com/Djangowon/TIL/blob/main/image/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-02-14%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%208.35.59.png" height=80% width=80%>
    
    
#### FastAPI 와 uvicorn 을 설치하기
```
$ pip install fastapi
```
```
$ pip install uvicorn[standard] 
```
uvicorn을 통해 python 서버를 실행시킬 수 있음, [standard] 옵션은 생략해도 무방함

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
#### 웹 서버를 열어 확인
[http://127.0.0.1:8000/](http://127.0.0.1:8000/)  
```
{"message": "Hello World"}
```
<img src="https://github.com/Djangowon/TIL/blob/main/image/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-02-14%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%208.37.55.png" height=80% width=80%>

Hello World가 잘 출력됩니다.

#### swagger를 통해 확인해보기
[http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs/)  
