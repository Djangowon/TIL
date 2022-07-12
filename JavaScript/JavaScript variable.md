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

## Ref
