# Spread Operator

<br>
<br>

## ... spread operator
* Array에 붙이면 대괄호를 제거해줌
* 문자에 붙이면 펼쳐줌, 각 문자 하나씩 다 해체시켜줌
* 중괄호, 대괄호, 소괄호 안에서만 사용하는 문법

<br>
<br>


## spread operator 쓸만한 곳

```javascript
const a = [1,2,3];
const b = [4,5];

const c = [...a, ...b];
```
* 어레이 합치기 / 복사할 때 유용함


<br>
<br>


```javascript
const a = [1,2,3];
const b = a;

a[3] = 4;

console.log(a); // [1,2,3,4]
console.log(b); // [1,2,3,4]
```
* Deep copy(독립적인 자료로 복사)할 때 유용함
* reference data type(Array, Object)들은 그냥 등호로 복사하면 값을 공유함
* 각각 독립적인 값을 가지도록 Array, Object를 복사할 때 spread operator 사용

```javascript
const a = [1,2,3];
const b = [...a];

a[3] = 4;

console.log(a); // [1,2,3,4]
console.log(b); // [1,2,3]
```


<br>
<br>



```javascript
const o1 = {a:1, b:2};
const o2 = {...o1, a:2}

console.log(o2); // {a:2, b:2}
```

* 오브젝트 합치기 / Deep copy
* 오브젝트를 spread operator로 카피하다가 값 중복이 일어나는 경우, 가장 뒤에 있는 값을 적용시킴


<br>
<br>


```javascript
function add(a,b,c) {
	console.log(a+b+c)
}

const al = [10,20,30];
add(al[0], al[1], al[2]); //복잡하게 해체하는 법

add.apply(undefined, al); //옛날 방식 이상한 함수써서 해체하는 법
add(...al); //스프레드 오퍼레이터로 해체하는 법
```
* 함수 파라미터 넣는 경우
* array 내의 모든 데이터를 파라미터로 집어놓고 싶은 경우

> apply함수는 파라미터로 array 집어넣기 가능하기 때문에 옛날에 저렇게 씀

<br>
<br>


## apply 함수
```javascript
const person = {
	hello : function() {
		console.log(this.name + " Hi")
	}
}

const person2 = {
	name : 'SON'
}

person.hello.apply(person2) // SON HI

person.hello.apply(person2, [1,2]) 
person.hello.call(person2, 1,2) 
```

* apply() 는 함수 옮겨와서 실행시켜주는 함수임
* apply / call 비슷한데, apply는 파라미터를 array 형태로 집어넣기 가능


<br>
<br>


## Ref
https://codingapple.com/course/javascript-es6/
