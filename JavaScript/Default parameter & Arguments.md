# Default parameter & Arguments


<br>
<br>


## 함수의 default 파라미터
* 자바스크립트는 파라미터가 2개 들어가는 함수인데 1개만 써도 에러가 안나는 언어임
* 파라미터에 아무값도 안넣을 경우 디폴드값을 줄 수 있음
* 수학연산자 사용 가능
* 함수도 가능

```javascript
function plus(a, b = 7 * a) {
    console.log(a + b)
}

plus(1); // 8
```



<br>
<br>


## 함수의 arguments
* 모든 파라미터를 한꺼번에 싸잡아서 다루고 싶을 경우 사용함
* arguments는 함수에 들어온 파라미터를 전부 Array로 감싸주는 변수같은 것임
* 함수 안에서 사용할 수 있는 미리 정의된 키워드 혹은 변수라고 보면 됨

```javascript
function func(a,b,c){
  for (var i = 0; i < arguments.length; i++){
    console.log(arguments[i])
  }
}

ar(2,3,4); // 2 3 4 차례대로 출력됨
```

### arguments의 단점
* array로 파라미터를 전부 담아놓았는데 파라미터 중 일부만 사용하고 싶으면 arguments라는 자료를 쪼개서 사용해야 함(일반 array처럼)
* arguments는 옛날 문법임 -> 최신 문법 ES6 Rest 파라미터


<br>
<br>

## ES6 Rest 파라미터
* arguments는 파라미터 자리에 오는 모든 파라미터를 []에 담아줌
* Rest 파라미터는 ...뒤에 오는 모든 파라미터를 []에 담아줌
* 함수 파라미터 자리에 ...이 붙으면 rest / 나머지 경우 spread operator임
```javascript
function func2(a, b, ...rest){
    console.log(rest)
}

func2(1,2,3,4,5,6,7,8); // [3,4,5,6,7,8]
```

### ...rest 파라미터 주의점
* 파라미터 가장 마지막에만 사용가능
* 두번 이상 사용 못 함, 한번만 사용 가능


<br>
<br>


## Ref
https://codingapple.com/course/javascript-es6/
