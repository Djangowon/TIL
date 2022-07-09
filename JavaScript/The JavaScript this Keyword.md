# The JavaScript this Keyword


<br>

## this
* JavaScript에서 함수의 this 키워드는 다른 언어와 조금 다르게 동작함
* this 키워드는 객체를 나타내고, this 의 뜻은 사용하는 상황에 따라 뜻이 3-4개 정도 됨 
* 어떤 this 개체가 호출되는 지에 따라 다름. 즉, 사용 방법에 따라 다른 개체를 참조함


<br>

## 1. 일반함수 안에서 this는 {window}
* 그냥 사용하거나 일반함수 안에서 this는 {window}라는 object를 나타냄
* window는 기본 함수들의 수납공간
* script 안의 자바스크립트 코드들은 사실 window라는 {}로 감싸져 있는 형태임


```html
<script>
console.log(this)

function hello () {
console.log(this)
}
</script>
```


<br>

### strict mode
> strict mode => 자바스크립트를 엄격하게 쓸 수 있음  

* strict mode + 일반함수 내에서 this는 undefined
```html
<script>
'use strict'; // 이 코드가 최상단에 있을 때 => JavaScript Strict Mode
</script>

```

<br>
<br>

## 2. object 내 함수 안에서 this는 메소드의 주인님
* 해당 함수를 가지고 있는 object를 나타냄, 즉, 나를 포함하고 있는 object.

```js
const obj= {data:"hhh", hello: function world() {console.log(this)}}

obj.hello(); // 그냥 obj 그 자체를 나타냄. this는 메소드를 가지고 있는 오브젝트!(메소드의 주인님)
```
* 화살표 함수는 this값을 함수 밖에 있던 것 그대로 가져다 씀 

* 함수나 변수를 전역공간에서 만들면 {window}에 보관하고, window는 global object임
    * window = 모든 전역변수, 함수, DOM을 보관하고 관리하는 전역객체

<br>

* 결론: 즉, this는 나를 담고있는 오브젝트를 나타내므로 1,2번 뜻이 사실은 같은 의미였단 것을 알 수 있음


<br>
<br>

## 3. constructor 안에서 this는 새로 생성되는 object
* constructor 메소드는 클래스의 인스턴스 객체를 생성하고 초기화하는 메소드
* constructor는 정해진 key:value를 가진 객체를 편리하게 생성할 수 있게 도와주는 기계같은 역할
* constructor 문법으로 this를 쓰면 this는 새로 생성되는 object를 나타냄

```js
function Person(name, language) {
    this.name = name;
    this.language = language;
    this.info = function () {
        console.log(`이름: ${name} 언어: ${language}`);
    };
}
```
* 위와 같이 constructor는 대문자로 시작하는 규칙
* this로 접근하여 키 값을 할당해줌

```js
let person1 = new Person('손석구','JavaScript')
```
* new 생성자명(파라미터값)을 이용하여 객체(인스턴스)를 만들어 줌
```js
person1.info() // 이름: 손석구 언어: JavaScript
```

<br>
<br>


## 4. Event Listener 안에서 this는 e.currentTarget
* e.currentTarget 즉, 지금 이벤트가 동작하는 곳
```js
document.getElementById('버튼').addEventListener('click', function(e){
  console.log(this)
});
```

<br>
<br>


### 이벤트리스너 내 콜백함수 안에서 this를 쓰거나, 오브젝트 내 콜백함수 안에서 this를 쓰는 경우
```js
document.getElementById('button').addEventListener('click', function(e){
  const array = [1,2,3];
  array.forEach(function(){
    console.log(this)
  });
});
```
* 위의 예제에선 eventlistener내부는 맞지만 그 안에서 function을 하나 더 만났기 때문에 의미가 변함
* function() {console.log(this)}는 그냥 일반함수이기 때문에 {window}가 출력됨

<br>


* this값을 판단할 땐 가장 가까이 있는 함수를 살펴보면 됨
* 즉, this값은 function을 만날 때마다 바뀔 수 있기 때문에 원하는 this 값을 쓰기가 힘들 수 있음, 그럴 때 arrow function을 쓰면 됨!

<br>

### arrow function
* JavaScript ES6 문법 중, function () {} 대신 쓸 수 있는 () => {} 이라는 arrow function 문법
* 내부의 this값을 변화시키지 않음
* 외부 this 값 그대로 재사용 가능함

<br>

* 결론: this의 값은 this가 어떤 함수 안에 들어있는 지만 잘 체크하면 바로 알 수 있음

<br>
<br>


## Ref
https://codingapple.com/course/javascript-es6/  
https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/this  
https://www.w3schools.com/js/js_this.asp  
https://velog.io/@hoon_dev/JavaScript-constructor%EC%83%9D%EC%84%B1%EC%9E%90-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0  
