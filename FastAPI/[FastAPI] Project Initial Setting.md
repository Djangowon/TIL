# Project Initial Setting
```
$ pip install fastapi
```
```
$ pip install uvicorn[standard]
```
```python
$ vi main.py

from fastapi import FastAPI

app = FastAPI()


@app.get("/")
async def root():
    return {"message": "Hello World"}
```
```
$ uvicorn main:app --reload # 로컬에서 run
$ uvicorn main:app --reload --host=0.0.0.0 --port=8000 # +모든 접근 가능, 포트번호 설정할 때
```
[http://127.0.0.1:8000/](http://127.0.0.1:8000/)  
```
{"message": "Hello World"}
```
[http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs/)  
swagger를 통해 확인해보기
