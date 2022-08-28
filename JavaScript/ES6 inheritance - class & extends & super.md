# ES6 inheritance - class & extends & super

<br>
<br>

## class
* class 문법은 constructor, prototype을 이용한 상속기능을 보기 쉽게 만들 수 있도록 도와주는 문법임

```javascript
class parent {
	constructor() {
		this.name = "aaa";
	}
}

let child = new parent();
```


### Object.getPrototypeOf()
* 부모의 prototype을 출력해줌
* \__proto__ 키워드와 비슷한 역할


<br>
<br>

## extends
* 유사한 class를 만들고 싶을 때, 상속받아 쓰고 싶을 때 사용하는 extends 문법
* 속성을 그대로 물려받아서 사용 가능함
* extends 해서 만든 class는 this 키워드를 그냥 쓸 수 없음 -> super(); 다음에 써야함
	
<br>

```javascript
class grandFather {
	constructor(name) {
		this.lastName = "Jang";
		this.FirstName = name;
	}
	sayHi(){ console.log('안녕 나는 할아버지') }
}


class father {
	constructor() {
		super(name);
		this.age = 55;
	}
	sayHi2() { 
	console.log('안녕 나는 아버지');
	super.sayHi(); 
	}
}

```


<br>
<br>


## super()
* super()는 extends로 상속중인 부모 class의 constructor()" 를 의미함

<br>

### super() 의 또 다른 용도
* 부모 class의 prototype 가져다쓰기 가능함
* super()의 두가지 의미
	1. constructor 안에서 쓰면 부모 class의 constructor 
	2. prototype 함수 안에서 쓰면 부모 class의 prototype


<br>
<br>

## Ref
https://codingapple.com/course/javascript-es6/
