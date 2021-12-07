# HTTP Request/ Response message
## HTTP request message 구조
HTTP 요청은 프론트엔드(클라이언트) 에서 백엔드(서버)에 일(데이터 처리)을 시작하게 하기 위해 보내는 메세지다. 이 메세지의 구조는 크게 세 부분으로 구성되어있다. 
#### Start Line
```python
1. HTTP Method: 해당 요청이 의도한 액션을 정의하는 부분. 주로 GET, POST, DELETE가 많이 쓰임
2. Request target: 해당 request가 전송되는 목표 url 
3. HTTP Version: 말 그대로 사용되는 HTTP 버전을 뜻한다. 주로 1.1 버전이 널리 쓰임

GET /login HTTP/1.1
해석: GET 메소드로 login 이라는 요청 타겟에 HTTP 1.1 버전으로 요청을 보내겠다!
```
#### Headers
해당 요청에 대한 추가 정보(메타 데이터)를 담고있는 부분이다. 
```python
Key: Value 값으로 되어있다 (JavaScript의 객체, Python의 딕셔너리 형태라고 보면 된다)
자주 사용되는 Headers 의 정보에는 다음이 있다 

Headers: {
	Host: 요청을 보내는 목표(타겟)의 주소. 즉, 요청을 보내는 웹사이트의 기본 주소가 된다
	(ex. www.apple.co.kr)
	User-Agent: 요청을 보내는 클라이언트의 대한 정보 (ex. chrome, firefox, safari, explorer)
	Content-Type: 해당 요청이 보내는 메세지 body의 타입 (ex. application/json)
	Content-Length: body 내용의 길이
	Authorization: 회원의 인증/인가를 처리하기 위해 로그인 토큰을 Authroization 에 담는다
}
```
#### Body
해당 요청의 실제 내용. 주로 Body를 사용하는 메소드는 POST다. 
```python
ex) 로그인 시에 서버에 보낼 요청의 내용
Body: {
	"user_email": "wecode@gmail.com"
	"user_password": "wecode"
}
```
## HTTP response message 구조
HTTP 규약에 따른 응답의 구조도 또한 크게 세 부분으로 구성되어있다.
#### Status Line
응답의 상태 줄이다. 응답은 요청에 대한 처리상태를 클라이언트에게 알려주면서 내용을 시작한다. 마치, 편지의 응답에 "응. 잘 지냈어" 라고 안부 인사를 건네는 것과 같다. 응답의 Status Line 도 세 부분으로 구성된다.
```python
1. HTTP Version: 요청의 HTTP버전과 동일
2. Status Code: 응답 메세지의 상태 코드
3. Status Text: 응답 메세지의 상태를 간략하게 설명해주는 텍스트

HTTP/1.1 404 Not Found
해석: HTTP 1.1 버전으로 응답하고 있는데, 프론트엔드에서 보낸 요청(ex. 로그인 시도)에 대해서
		 유저의 정보를 찾을 수 없기 때문에(Not Found) 404 상태 메세지를 보낸다.

HTTP/1.1 200 SUCCESS
해석: HTTP 1.1 버전으로 응답하고 있는데, 프론트엔드에서 보낸 요청에 대해서 성공했기 때문에
		 200 상태 메세지를 보낸다.
```
#### Headers
요청의 헤더와 동일하다. 응답의 추가 정보(메타 데이터)를 담고있는 부분이다. 다만, 응답에서만 사용되는 헤더의 정보들이 있다. (ex. 요청하는 브라우저의 정보가 담긴 User-Agent 대신, Server 헤더가 사용된다.)
#### Body
요청의 Body와 일반적으로 동일하다. 요청의 메소드에 따라 Body가 항상 존재하지 않듯이. 응답도 응답의 형태에 따라 데이터를 전송할 필요가 없는 경우엔 Body가 없을 수도 있다. 가장 많이 사용되는 Body 의 데이터 타입은 JSON(JavaScript Object Notation) 이다.
```python
ex) 로그인 요청에 대해 성공했을 때 응답의 내용
Body: {
	"message": "SUCCESS"
	"token": "kldiduajsadm@9df0asmzm" (암호화된 유저의 정보)
}
```
[참고](https://developer.mozilla.org/ko/docs/Web/HTTP/Messages/)
