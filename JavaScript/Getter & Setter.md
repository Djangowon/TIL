# Getter & Setter

<br>
<br>

## 함수만들어서 object 데이터 다루는 이유
> 1. 데이터를 꺼내거나, 수정하거나 할 때 편리함
> 2. 실수 방지 & 관리하기 쉬워짐
> 3. 데이터의 무결성, 데이터를 수정하기 전에 잘못된 데이터를 검사하고 싶을 때 쓰는 문법

<br>
<br>

* object 자료가 복잡할 때 편리함
	* 꺼내쓰는 법을 정의해두면 코드가 복잡해지지 않기 때문
* object 자료 수정시 편리함
	* object를 직접 변경하는 게 아니라 수정하는 함수를 정의해두고 사용함
	* 데이터 수정 시 미리 검사할 수 있음(안전장치 기능개발 가능)

* 함수사용할 때 소괄호 안쓰고 싶으면 get / set 키워드 사용하면 됨

<br>
<br>


## getter / setter

```javascript
class Unit {
  constructor() {
    this.hp = 100;
    this.cp = 5;
  }
  get battlePoint() {
    return this.hp + this.cp;
  }
  set heal(a) {
    this.hp = this.hp + a; 
  }
};

let unit1  = new Unit();

console.log(unit1.battlePoint);
unit.heal = 50; // set 키워드 사용했기 때문에 소괄호 없이 사용
```
<br>

## get / set 키워드 특징
* get 함수들 (getter)
	* return 이 있어야 함
* set 함수들 (setter)
	* 파라미터가 1개 있어야 함

<br>
<br>

## class에서 사용하는 get / set
* prototype 함수들에서도 get / set 가능

<br>
<br>

## Ref
https://codingapple.com/course/javascript-es6/
