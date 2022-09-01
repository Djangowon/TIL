# Destructuring

<br>
<br>


* 직관적으로 변수를 만들 수 있는 문법
```javascript
let [a, b, c] = [1, 2, 3];
```

<br>
<br>

* 등호로 default 변수 값을 지정할 수 있음
```javascript
let [a, b, c = 10] = [1, 2];
```

<br>
<br>

* object 데이터도 destrucruting 문법이 가능함
```javascript
let {name, age} = {name: "Do", age: 20};
```
* object는 array 처럼 위치를 맞춰준다기 보다 변수명을 key값과 똑같이 써야 함
* default 파라미터로 기본값 지정가능
```javascript
let {name : 이름 = 'dopa'} = { };
```

<br>
<br>


* 변수를 object로 집어넣고 싶은 경우
```javascript
let name = "paka";
let age = 30;

let obj = {name : name, age: age}
let obj = {name, age} //key, value값이 동일하면 이렇게 축약가능
```

<br>
<br>


* 함수 파라미터 만들 때도 destructuring 문법 사용가능함
	> 파라미터는 변수만드는 것과 똑같은 행위이기 때문에 변수만드는 문법을 파라미터에 그대로 적용할 수 있기 때문
```javascript
function func( { name, age }) { 
	console.log(name); 
	console.log(age); 
} 
	
let obj = { name : 'ralo', age : 20 };
func(obj);
```

<br>
<br>

## Ref
https://codingapple.com/course/javascript-es6/
