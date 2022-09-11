# ES8 async & await

<br>
<br>

> Promise: 순차적실행을 위해서 callback 함수 대신 쓸 수 있는 패턴

<br>
<br>

## async 

```javascript
async function plus() {
	return 1 + 1
}

plus().then(function(result) {
	console.log(result)
})
```


* asnyc를 function 앞에 붙이면 함수가 Promise 역할 가능
* 함수 실행 후에 Promise 오브젝트가 남음
* 단점은 성공 케이스만 가능함, 실패를 쓸 수 없음(강제로 실패는 가능)


<br>
<br>


## await

```javascript
async function plus() {
	const difficultArithmetic = new Promise((seccess, failure) => {
		failure();
	});

	try { let result = await difficultArithmetic }
	catch { difficultArithmetic Promise가 실패할 경우 실행 코드 }
}
```

* await = Promise 해결때까지 기다림(성공, 실패 판정 나올 때까지)
* await은 Promise 실패시 에러나고 멈춤
	* 방지하기 위해 try {} catch {} 사용함


<br>
<br>

## Ref
https://codingapple.com/course/javascript-es6/


