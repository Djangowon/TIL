# The JavaScript this Keyword


<br>

## this
* JavaScript에서 함수의 this 키워드는 다른 언어와 조금 다르게 동작함
* this 키워드는 객체를 나타내고, this 의 뜻은 사용하는 상황에 따라 뜻이 3-4개 정도 됨 
* 어떤 this 개체가 호출되는 지에 따라 다름. 즉, 사용 방법에 따라 다른 개체를 참조함


<br>

## 1. {window}
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

## 2. object 내 함수 안에서 this? 
* 해당 함수를 가지고 있는 object를 나타냄, 즉, 나를 포함하고 있는 object.

```js
const obj= {data:"hhh", hello: function world() {console.log(this)}}

obj.hello(); // 그냥 obj 그 자체를 나타냄. this는 메소드를 가지고 있는 오브젝트!(메소드의 주인님)
```
* 화살표 함수는 this값을 함수 밖에 있던 것 그대로 가져다 씀 

* 함수나 변수를 전역공간에서 만들면 {window}에 보관하고, window는 global object임
    * window = 모든 전역변수, 함수, DOM을 보관하고 관리하는 전역객체
* 결론: 즉, this는 나를 담고있는 오브젝트를 나타내므로 1,2번 뜻이 사실은 같은 의미였단 것을 알 수 있음


<br>
<br>


## Ref
https://codingapple.com/course/javascript-es6/  
https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/this  
https://www.w3schools.com/js/js_this.asp  
