# JavaScript variable 

<br>
<br>

## var, let, const
* 변수는 자료를 임시로 저장하는 공간
* object, array, function 등 모든 자료들을 담을 수 있음


||재선언|재할당|
|:--:|:--:|:--:|
|var|O|O|
|let|X|O|
|const|X|X|

* 완전 변경불가능한 오브젝트를 만둘고 싶은 경우? 
    * Object.freeze()  => 자바스크립트 기본함수
        > 소괄호에 오브젝트를 담으면 불변하는 특징이 있음, but 오브젝트 내의 오브젝트까지 freeze해주지는 않음

<br>
<br>

## variable scope
* 변수를 만들면 유효범위(존재범위)가 있음
* var 변수의 유효범위는 function
* let, const 변수의 유효범위는 거의 모든 중괄호임 (for, if, function 등)

<br>
<br>

## Hoisting
* 변수의 호이스팅 현상: 변수의 선언을 변수 범위 맨위로 끌고오는 현상
* 변수를 만나면 선언부분을 강제로 맨위로 끌어올림(자바스크립트 언어 자체 특징)
* 함수선언도 호이스팅 현상이 일어남

<br>
<br>

## 전역변수
* 모든 곳에서 쓸 수 있는 변수
* 바깥에 있는 변수는 안쪽에서 자유롭게 사용이 가능한데 이를 개발자용어로 참조가능하다라고 표현하고, 자바스크립트에서 이 현상을 closure라고 함

### window로 전역변수 만드는 법
```js
const 이름 = "손흥민";
window.나이 = 30;
```
* 전역변수를 만들 땐 var, let, const로 만드는 것보다 window로 만들어주는 것을 좀 더 권장함
* window로 만드는 것이 좀 더 전역변수스럽기 때문에, 코드가 많아졌을 때 전역변수와 지역변수를 구분하기 쉬움

<br>
<br>

## Ref
https://codingapple.com/course/javascript-es6/
