# Basic Grammar
## 01. Print
파이썬에서 출력하는 방법은 print() 

```python 
print("Hello World!")
print("함께해서 Wecode")
```

## 02. Data Types
* String = 문자열
* Integer = 정수
* Float = 소수점 숫자
* Complex Numbers = 실수와 허수를 포함하고 있는 복소수. 파이썬에서는 j를 사용하여 허수를 표현한다.  
ex) 1+3j, 2-4j
* Boolean = True / False

## 03. Variables For Strings, Numbers
파이썬에서 변수는 데이터의 별명(식별자)
#### 변수 이름 법칙
* 변수 이름은 영어 알파벳, 숫자, underscore(\_) 로만 구성.
* 변수 이름 첫글자는 알파벳 or underscore(\_) 로만 시작, 숫자로 시작할 수 없음.
* 영어 알파벳 대소문자 구분됨.  
* 변수에 저장할 수 있는 값은 string(문자열), integer(정수), floating(부동 소수점), 음수 모두 가능.

## 04. Arithmetic Operators
#### 산술 연산자
* \+ (더하기)
* \- (빼기)
* \* (곱하기)
* \/ (나누기)
* \// (몫)
* \% (나머지)
* \** (제곱)

## 05. Assignment Operators
#### 할당 연산자
* \= (왼쪽 변수에 오른쪽 값을 할당)
* \+= (왼쪽 변수에 오른쪽 값을 더하고 결과를 왼쪽변수에 할당)
* \-= (왼쪽 변수에서 오른쪽 값을 빼고 결과를 왼쪽변수에 할당)
* \*= (왼쪽 변수에 오른쪽 값을 곱하고 결과를 왼쪽변수에 할당)
* \/= (왼쪽 변수에서 오른쪽 값을 나누고 결과를 왼쪽변수에 할당)
* \%= (왼쪽 변수에서 오른쪽 값을 나눈 나머지의 결과를 왼쪽변수에 할당)
* \*\*= (왼쪽 변수에 오른쪽 값만큼 제곱을 하고 결과를 왼쪽변수에 할당)
* \//= (왼쪽 변수에서 오른쪽 값을 나눈 몫의 결과를 왼쪽변수에 할당)
#### 수학 연산 표현 순서
1. \(&nbsp;&nbsp;\)
2. \*\*
3. \*,&nbsp; \/,&nbsp; \%
4. \+,&nbsp; \-  
  
* 연산의 순서는 혼동되기 쉽고 버그가 날 수 있는 요인이 될 수 있음.  
* 괄호 적절히 사용해 명확하게 해주는 것이 코드의 가독성을 높일 수 있다.

## 06. f-string, Literal String Interpolation
문자열에 f 또는 F 접두어를 붙이고 표현식을 {expression\}로 작성하여 문자열에 파이썬 표현식의 값을 삽입할 수 있게 함.
#### 사용법
* 따옴표 앞에 f를 붙인다.
* 치환하고 싶은 변수(혹은 함수 호출)를 \{\}를 사용해서 표시한다.
```python 
name = input()
print(f"hello, {name}")
```