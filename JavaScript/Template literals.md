# Template literals

<br>
<br>

## backtick / backquote
```js
`문자 ${변수}`
```
* backquote 문자열의 장점
    * 엔터키 가능
    * 중간중간 변수 넣기 쉬움
    * 특히 HTML 작성시 유용함


<br>
<br>

## tagged literal
* 함수 뒤에 `` 붙여도 함수가 실행됨

```js

var 변수 = '손흥민';
var 문자 = `안녕하세요 ${ 변수 } 입니다`
function 해체분석기(문자들, 변수들) {
    console.log(문자들);
    console.log(변수들);
}

해체분석기`안녕하세요 ${ 변수 } 입니다`
```

* `문자`를 해체분석 할 수 있음
    * 단어 순서를 변경하거나, 단어를 제거하거나, ${변수} 위치를 옮기거나 쉽게 가능함
    * 해체분석용 함수를 만든 뒤에 파라미터 두개 넣어서 만들 수 있음
    * 해체분석기 함수의 첫번째 파라미터는 문자들을 array화 해주고, 두번째 파라미터는 ${변수}를 뜻함
    

<br>
<br>


## Ref
https://codingapple.com/course/javascript-es6/
