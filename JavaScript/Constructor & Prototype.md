## constructor 문법의 용도
* 비슷한 object 여러개 만들 때
* object 마구 복사하고 싶을 때 

```javascript
function Student() {
	this.name = "Kim";
	this.age = 15;
}

const stu1 = new Student();

```

* constructor 문법은 일반함수랑 다르게 관습적으로 대문자로 시작함
* this는 새로 생성되는 object를 뜻함(instance)


<br>
<br>

# prototype

* 프로토타입은 유전자임
* constructor를 만들면 prototype이라는 공간이 자동으로 생김(기계의 유전자)
* 프로토타입에 값을 추가하면 모든 자식들이 물려받기 가능함

<br>
<br>

## prototype 작동원리
* prototype에 추가한 데이터는 자식들이 자유롭게 사용 가능함
* 자바스크립트는 오브젝트에서 데이터를 뽑을 때 확인하는 순서가 있음
* 내가 직접 가지고 있는지 검사 -> 내가 가지고 있지 않다면 부모 유전자들을 차례대로 검사함
	> 1. 자식1에 출력하려는 값이 있는가?
	> 2. 자식1에 값이 없다면, 부모 유전자에 찾는 값이 있는가?
	> 3. 없다면, 부모의 부모 유전자에 값이 있는가? 
	> 4. 없다면, 부모의 부모의 부모의 유전자에 .. 있는가?

<br>
<br>

## prototype으로 상속 vs constructor로 상속 차이
* 자식들이 값을 직접 소유하게 만들고 싶으면 constructor로 상속시키면 됨
* 부모에게만 있고 그것을 자식들이 참조해서 쓰게 만들고 싶으면 prototype으로 상속시키면 됨
	> 보통 상속할 수 있는 함수 등을 prototype으로 많이 만들어놓음 
	
<br>
<br>

## prototype 특징
* 내 부모 유전자(부모의 prototype)를 검사하고 싶으면 \__proto__
* 반대로 생각하면 \__proto__ 를 이용해서(직접 등록) 부모 강제 등록(상속기능 구현)도 가능함

<br>
<br>

## Ref
https://codingapple.com/course/javascript-es6/
