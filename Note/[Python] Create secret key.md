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
`VERIFY SIGNATURE` -> `your-256-bit-secret` 안에 위에서 생성된 난수를 넣어줌
  
<img src="https://github.com/Djangowon/TIL/blob/main/image/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-01-06%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%201.37.19.png?raw=true/">
  
왼쪽에 밑줄 쳐진 encode 된 `_rzUh92Ez2fvSDZF-rrmTTTTH9FXD12JQTNAxRz5hRc` 를 쓰면 됨!
