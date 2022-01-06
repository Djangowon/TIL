# Create secret key
* 난수로 시크릿키 직접 만들기  
```
>>> from uuid import uuid4
```
```
>>> uuid4()
```
```
>>> UUID('bf5c0b29-7104-4858-934a-d57fb8d232e4')
```
[jwt.io](https://jwt.io/) 로 이동  
VERIFY SIGNATURE -> your-256-bit-secret 안에 위에서 생성된 난수를 넣어줌
