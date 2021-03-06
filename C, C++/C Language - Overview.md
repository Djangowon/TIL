# C Language - Overview

## C 언어란?
하드웨어의 독립적인 OS를 개발하기 위한 목적으로 만들어진 언어이다.
OS처럼 거대한 프로그램을 개발해야 하므로 체계적으로 구조화 된 특징이 있다.
확장성이 좋고 표현법이 다양하다.

#### 주요 용어
* 컴파일러(compiler): 프로그래밍 언어로 작성된 프로그램을 기계어로 바꿔주는 번역기
* 소스코드(source code): 프로그램 안에 있는 명령어
* 목적 파일(object file): .obj의 확장자를 갖는 파일로 기계어들의 집합으로 이루어진 파일
* 링커(linker): 여러 목적파일과 라이브러리 파일을 연결해주는 도구
* 예약어(reserved word): C 언어에서 미리 정의되어 있는 단어

## C언어의 정의, 역사, 특징
#### C언어의 정의
* 프로그래밍 언어
    * 사람과 컴파일러(compiler)가 이해할 수 있도록 약속된 형태의 언어 

#### Compiler
* 프로그래밍 언어로 작성된 프로그램을 컴퓨터가 이해할 수 있도록 기계어로 번역해 주는 번역기
    * 어셈블러(assembler): 기호로 표현된 어셈블리 코드를 기계어로 번역하는 번역기
    * 인터프리터(interpreter): 소스 프로그램을 한번에 기계어로 변환시키는 컴파일러와는 달리, 프로그램을 한 단계씩 기계어로 해석하여 실행하는 '언어처리 프로그램'

#### C언어의 역사
* Denis Ritchie(1972)
* Unix 운영체제 구현에 사용할 목적으로 개발
    * 컴퓨터 기종간 호환성을 가진 고급이면서, 하드웨어를 제어할 수 있는 새로운 언어가 필요함
* 어셈블리 언어로 된 UNIX 운영체제가 거의 C언어로 대체됨 

#### C언어의 특징
* 프로그램 이식성이 높음
* 간단한 문법 표현으로 함축적인 프로그램 작성이 가능
* 저급언어 특성을 가진 고급언어

## C 프로그램의 완성 과정
코딩 -> 컴파일 -> 링킹
* 코딩
    * 주어진 문제에 대한 설계를 바탕으로 소스코드(source code)를 작성하여 소스파일(source file)을 생성하는 과정
* 컴파일(compile) 단계
    * 소스파일이 목적파일(object file)로 변환되는 과정
        * 소스파일(.c)을 목적파일(.obj)로 번역하는 과정으로 이 과정을 담당하는 프로그램을 '컴파일러'라고 함
* 링킹(linking) 단계
    * 목적파일을 실행파일(execution file)로 변환하는 과정
        * 목적파일(.obj)을 실행파일(.exe)로 번역하는 과정으로 이 과정을 담당하는 프로그램을 '링커'라고 함 

* build 혹은 make
    * 컴파일과 링크를 합친 과정으로 즉, 컴파일 후 링크를 의미


* 목적파일의 필요성
    > 소스파일에서 실행파일로 바로 번역한다고 가정해보겠습니다.  
    100만줄짜리 소스파일에서 1줄만 수정한 후 실행파일로 다시 번역한다고 해보겠습니다.  
    1줄이 수정됐으므로 100만줄을 다시 번역해야합니다. 이는 굉장히 비효율적입니다.  
    그렇다면 소스파일을 100등분 해보겠습니다. 각 파일은 1만줄씩 있을겁니다.  
    1줄이 수정됐다면 그 1줄에 해당되는 1만줄짜리 파일만 번역하면 됩니다. 이 방법이 더욱 효율적이기 떄문에 이 방법을 사용합니다.  
    그렇지만 한가지 문제점이 생겼습니다. 소스파일을 여러개로 분할하게 되면 실행파일로 바로 번역이 불가능합니다.  
    따라서 중간단계를 한번 거쳐야 하는데 이 중간단계가 바로 목적파일입니다.


## C 프로그램의 기본 구조
* C 프로그램은 반드시 하나 이상의 함수를 포함해야 한다.
* main()가 반드시 존재해야 한다.
* 함수의 시작과 끝을 알리는 {}를 사용해야 한다.
* 중괄호 안에는 변수 선언문, 치환문, 연산문, 함수 등의 명령을 기입한다.
* 선행처리기(proprocessor)를 제외하고 문장의 끝에는 세미콜론을 붙인다.

## C 프로그램의 구성 요소
* 예약어(reserved)
    * 자료형 : char, int, float, short, long, double, unsigned, union, enum, void, ...
    * 기억 : auto, static, extern, register, ...
    * 제어 : ifelse, for, while, dowhile, wditch~case, break, continue, return, ...
    * 기타 : main, sizeof, include, ...
* 명칭(idnetifier) : 변수, 배열, 함수, ... 등의 이름
    * 규칙
        * 영문자, 숫자의 조합
        * 명칭의 첫 문자는 영문자나 _ 이어야 함
        * _이외의 특수문자 사용 X
        * 문자 사이에 공백 X
        * 예약어 사용 X
        * 대소문자는 구별하여 사용
        * 명칭의 길이는 컴파일러에 다라 차이가 있음 (일반적으로 32자)
* 상수 : 값이 불변인 자료
* 연산자 : =, -, *, /, ++, ...
    * 다른 언어에 비해 연산자가 많음
* 설명문 : 프로그램에 대한 주석
    * /**/, //

## 에러와 경고
#### 에러
* C 언어의 문법상 잘못된 경우 에러
* C 언어 문법에 맞지 않은 형식의 사용이나, 반드시 필요한 지정이 빠진 경우 발생
* 에러 메세지를 확인하여 반드시 수정해야 함

#### 경고
* 경미한 실수
* 큰 문제는 없지만, 이식성에 문제가 생기거나, C 언어 문법에서 권장하지 않은 방법으로 소스를 작성했을때 경고
* 무시해도 상관 없음


[Ref](https://jeaha.dev/83/)  
[Ref](https://turtlog.tistory.com/3/)
