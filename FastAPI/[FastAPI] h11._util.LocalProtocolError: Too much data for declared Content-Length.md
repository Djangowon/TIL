# h11._util.LocalProtocolError: Too much data for declared Content-Length

기존의 return에 message만 반환하던 코드에서 JSONResponse로 리팩토링 하던 중 204를 반환할 때만 에러가 나왔다.
```
INFO:     127.0.0.1:53000 - "DELETE /users/12 HTTP/1.1" 204 No Content
ERROR:    Exception in ASGI application
Traceback (most recent call last):
  File "/opt/homebrew/Caskroom/miniconda/base/envs/payhere/lib/python3.9/site-packages/uvicorn/protocols/http/h11_impl.py", line 373, in run_asgi
    result = await app(self.scope, self.receive, self.send)
  File "/opt/homebrew/Caskroom/miniconda/base/envs/payhere/lib/python3.9/site-packages/uvicorn/middleware/proxy_headers.py", line 75, in __call__
    return await self.app(scope, receive, send)
  File "/opt/homebrew/Caskroom/miniconda/base/envs/payhere/lib/python3.9/site-packages/fastapi/applications.py", line 208, in __call__
    await super().__call__(scope, receive, send)
  File "/opt/homebrew/Caskroom/miniconda/base/envs/payhere/lib/python3.9/site-packages/starlette/applications.py", line 112, in __call__
    await self.middleware_stack(scope, receive, send)
  File "/opt/homebrew/Caskroom/miniconda/base/envs/payhere/lib/python3.9/site-packages/starlette/middleware/errors.py", line 181, in __call__
    raise exc
  File "/opt/homebrew/Caskroom/miniconda/base/envs/payhere/lib/python3.9/site-packages/starlette/middleware/errors.py", line 159, in __call__
    await self.app(scope, receive, _send)
  File "/opt/homebrew/Caskroom/miniconda/base/envs/payhere/lib/python3.9/site-packages/starlette/middleware/cors.py", line 84, in __call__
    await self.app(scope, receive, send)
  File "/opt/homebrew/Caskroom/miniconda/base/envs/payhere/lib/python3.9/site-packages/starlette/exceptions.py", line 82, in __call__
    raise exc
  File "/opt/homebrew/Caskroom/miniconda/base/envs/payhere/lib/python3.9/site-packages/starlette/exceptions.py", line 71, in __call__
    await self.app(scope, receive, sender)
  File "/opt/homebrew/Caskroom/miniconda/base/envs/payhere/lib/python3.9/site-packages/starlette/routing.py", line 656, in __call__
    await route.handle(scope, receive, send)
  File "/opt/homebrew/Caskroom/miniconda/base/envs/payhere/lib/python3.9/site-packages/starlette/routing.py", line 259, in handle
    await self.app(scope, receive, send)
  File "/opt/homebrew/Caskroom/miniconda/base/envs/payhere/lib/python3.9/site-packages/starlette/routing.py", line 64, in app
    await response(scope, receive, send)
  File "/opt/homebrew/Caskroom/miniconda/base/envs/payhere/lib/python3.9/site-packages/starlette/responses.py", line 139, in __call__
    await send({"type": "http.response.body", "body": self.body})
  File "/opt/homebrew/Caskroom/miniconda/base/envs/payhere/lib/python3.9/site-packages/starlette/exceptions.py", line 68, in sender
    await send(message)
  File "/opt/homebrew/Caskroom/miniconda/base/envs/payhere/lib/python3.9/site-packages/starlette/middleware/errors.py", line 156, in _send
    await send(message)
  File "/opt/homebrew/Caskroom/miniconda/base/envs/payhere/lib/python3.9/site-packages/uvicorn/protocols/http/h11_impl.py", line 469, in send
    output = self.conn.send(event)
  File "/opt/homebrew/Caskroom/miniconda/base/envs/payhere/lib/python3.9/site-packages/h11/_connection.py", line 468, in send
    data_list = self.send_with_data_passthrough(event)
  File "/opt/homebrew/Caskroom/miniconda/base/envs/payhere/lib/python3.9/site-packages/h11/_connection.py", line 501, in send_with_data_passthrough
    writer(event, data_list.append)
  File "/opt/homebrew/Caskroom/miniconda/base/envs/payhere/lib/python3.9/site-packages/h11/_writers.py", line 58, in __call__
    self.send_data(event.data, write)
  File "/opt/homebrew/Caskroom/miniconda/base/envs/payhere/lib/python3.9/site-packages/h11/_writers.py", line 78, in send_data
    raise LocalProtocolError("Too much data for declared Content-Length")
h11._util.LocalProtocolError: Too much data for declared Content-Length
```
삭제는 잘 되지만 저 LocalProtocolError가 나와서 찾아보았다.

HTTP 204 내용 없음은 메시지 본문을 포함할 수 없다. https://tools.ietf.org/html/rfc7230#section-3.3.3  
"HEAD 요청에 대한 모든 응답 및 1xx(정보용), 204(내용 없음) 또는 304(수정되지 않음) 상태 코드는 메시지에 있는 헤더 필드에 관계없이 항상 헤더 필드 뒤의 첫 번째 빈 줄에서 종료되므로 메시지 본문을 포함할 수 없다."

내용 길이는 h11에서 강제로 0( h11._connection.py:75)과 같으므로 이 끝점에서 무언가를 반환하면 예외가 발생한다.  

204 상태 코드를 반환하는 유효한 끝점을 만들려면 Response 개체를 사용해야 한다.

```python

@router.post('/users/signup')
async def post_user(user_name: str, email: str, password: str):
    await create_user(user_name=user_name, email=email, password=password)
    return JSONResponse(status_code=201, content={"message": "CREATE_SUCCESS"})


@router.put('/users/{user_id}')
async def patch_user(user_id: int, users: User):
    await update_user(user_id, users)
    return JSONResponse(status_code=200, content={"message": "UPDATE_SUCCESS"})


@router.delete('/users/{user_id}')
async def delete_user(user_id: int):
    await remove_user(user_id)
    return Response(status_code=HTTPStatus.NO_CONTENT.value) # 여기
```
** 따라서 post와 put과 다르게 delete에는 JSONResponse 대신 Response를 적용시킨 코드

[Ref](https://github.com/tiangolo/fastapi/issues/2253/)
