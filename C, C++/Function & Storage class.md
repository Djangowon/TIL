# Function & Storage class
## 함수의 개념
### 함수
* 함수란 특정한 작업(기능)을 수행하도록 설계된 독립적인 프로그램
* 이러한 함수들이 정해진 순서에 따라 실행됨으로써 프로그램의 기능을 수행

### C프로그램은 함수들로 구성
* 전체의 실행 내용을 몇 개의 모듈(module)로 분류
* 각각의 모듈에 해당하는 내용을 함수로 작성
* 실행순서에 따라 그 함수들을 차례로 호출하여 실행

### 함수의 특성
* 함수들은 서로를 자유로이 호출 가능
* 모든 함수는 서로 독립적

### 함수의 장점
* 프로그램의 수정이 용이하다.
* 함수 재사용으로 코드 중복을 최소화한다.
* 프로그램의 기능을 한 눈에 파악할 수 있게 해줌으로써 유지관리가 쉽다.

#### ex) 단위 프로그램을 하나의 함수에 기술한 경우
* 함수의 길이가 커짐
* 프로그램의 가독성 문제
* 수정의 어려움
* 일부분만 재호출 어려움

> 결국, 기능별 독립된 단위(함수)로 구성하는 것이 효율적임

## 표준 함수
* C언어에서의 함수
    * 표준함수: C언어 자체에서 제공하는 함수
    * 사용자 정의함수: 사용자가 정의하여 사용하는 함수

* 표준 함수
    * `표준함수의 원형`은 헤더파일에 정의
    * `표준함수의 실체`는 라이브러리 파일에 수록
    * `표준함수를 사용하려면` 원형이 선언되어 있는 헤더파일을 `#include` 시켜 주어야 함

### 표준함수의 원형 예시
#### printf(), scanf() 함수의 원형
```
int printf(const char *format, ・・・);
int scanf(const char *format, ・・・);
```
* 헤더파일에 정의되어 있음(stdio.h)
* 표준함수를 사용하려면 stdio.h를 #include

#### sin(), cos() 함수의 원형
```
double sin(double x);
double cos(double x);
```
* 헤더파일에 정의되어 있음(math.h)
* 표준함수를 사용하려면 math.h를 #include

### C언어에서의 표준함수 예시
|헤더파일|선언된 함수|함수 예시|
|:---:|:---:|:---|
|stdio.h|입출력함수|printf(), scanf(), getchar(), putchar()|
||파일관련 함수|fopen(), fclose(), fprintf(), ・・・|
|conio.h|콘솔 입출력함수|putch(), cputs(), cprintf(), getch(), getche(), cscanf(), ・・・|
|string.h|문자열처리 함수|strcat(), strcmp(), strcpy(), strlen(), strncat(), strncpy(), ・・・|
|math.h|수학 함수|sqrt(), sin(), cos(), tan(), log(), exp(), pow(), abs(), asin(), acos(), atan() cosh(), ・・・|
|ctype.h|문자형태 판별함수|isalpha(), isdigit(), islower(), ・・・|
||문자변환 함수|tolower(), toupper()|
|stdlib.h|수치변환 함수|atoi(), itoa()|
||난수관련 함수|rand(), srand()|
||정렬/검색 함수|qsort(), lfind()|


