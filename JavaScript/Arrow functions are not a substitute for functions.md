# Arrow functions are not a substitute for functions


<br>
<br>

## Arrow function
* ES6 문법 이후부터는 자바스크립트에서 함수를 만들 수 있는 문법 () => {}
* 화살표 함수는 전통적인 함수(function)의 간편한 대안이고, 함수를 대체하는 것은 아님
* 화살표 함수는 몇 가지 제한이 있고 모든 상황에 사용할 수는 없음
    * this나 super에 대한 바인딩이 없고, methods 로 사용될 수 없음
    * new.target키워드가 없음
    * 일반적으로 스코프를 지정할 때 사용하는 call, apply, bind methods를 이용할 수 없음
    * 생성자(Constructor)로 사용할 수 없음
    * yield를 화살표 함수 내부에서 사용할 수 없음

<br>
<br>

##  Arrow function을 쓰는 이유
* 함수 본연의 기능을 잘 표현하는 문법임, arrow function을 사용하면 함수 본연의 입출력 기능을 아주 직관적으로 잘 표현함
    > 함수의 입출력 기능: input을 집어넣으면 output을 출력해주는 것 (소괄호에 뭔가 집어넣으면 return을 이용해 뭔가 뱉어내는 것)

