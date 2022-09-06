# ES6 Promise

<br>
<br>

```javascript
const promise = new Promise();

promise.then(function() {

}).catch(function() {

});
```

* promise는 코드/함수의 디자인 패턴이고, 성공/실패 판정하는 기계임
* callback함수 디자인패턴이 맘에 안 들면 promise 디자인패턴을 사용해도 됨

<br>
<br>


## Promise > callback ?
* callback 대신 예쁜 코드를 쓸 수 있음
	> callback 함수와 다르게 옆으로 코드가 길어지지 않음. then 함수 붙여서 순차적으로 실행함
* 성공/실패의 경우에 맞춰서 각각 다른 코드 실행 가능함
	> 성공하면 then(), 실패하면 catch()
* 비동기적 처리가 가능하게 만들어주는 문법 아님(Promise에 대한 오해)

<br>
<br>

## Promise 3가지 상태
* \<resolved> 성공
* \<pending> 판정 대기 중
* \<rejected> 실패

<br>


### Promise가 적용된 곳들
* fetch()
* jQuery.ajax()


<br>
<br>



## Ref
https://codingapple.com/course/javascript-es6/
