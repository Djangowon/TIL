# 문제
두 개의 input에는 복소수(complex number)가 string 으로 주어집니다.
복소수란 a+bi 의 형태로, 실수와 허수로 이루어진 수입니다.

input으로 받은 두 수를 곱해서 반환해주세요.
반환하는 표현도 복소수 형태의 string 이어야 합니다.

복소수 정의에 의하면 (i^2)는 -1 이므로 (i^2) 일때는 -1로 계산해주세요.

* 제곱 표현이 안 되어 i의 2제곱을 (i^2)라고 표현했습니다.

&nbsp

## 예제 1:
Input: "1+1i", "1+1i"
Output: "0+2i"
설명: 
(1 + i) * (1 + i) = 1 + i + i + i^2 = 2i 
2i를 복소수 형태로 바꾸면 0+2i.

&nbsp

## 예제 2:
Input: "1+-1i", "1+-1i"
Output: "0+-2i"
설명: 
(1 - i) * (1 - i) = 1 - i - i + i^2 = -2i, 
-2i를 복소수 형태로 바꾸면 0+-2i.

&nbsp

## 예제 3:
Input: "1+3i", "1+-2i"
Output: "7+1i"
설명: 
(1 + 3i) * (1 - 2i) = 1 - 2i + 3i -6(i^2) = 1 + i + 6, 
7+i를 복소수 형태로 바꾸면 7+1i.

&nbsp

## 가정
input은 항상 a+bi 형태입니다.
output도 a+bi 형태로 나와야 합니다.

## split 함수
문자열을 나눌 때 사용한다. 괄호 안에 아무것도 넣지 않으면 공백(띄어쓰기, 탭 등)을 기준으로 문자열을 나눈다. 나누어진 값은 리스트의 요소로 저장되는데, 분할된 문자의 개수만큼 각각을 변수로 지정하는 것도 가능하다. 
#### 사용예시
```python
test = 'Hello world : 헬로 월드'
print(test)
print(test.split())
print(test.split(sep=':'))
print(test.split(maxsplit=1))
print(test.split(maxsplit=2))
print(test.split(maxsplit=3))

-- 출력값
Hello world : 헬로 월드
['Hello', 'world', ':', '헬로', '월드']	# 기본값으로 분할
['Hello world ', ' 헬로 월드']	# ':'기준 분할
['Hello', 'world : 헬로 월드']	# 공백기준, 1번 분할
['Hello', 'world', ': 헬로 월드']	# 공백기준, 2번 분할
['Hello', 'world', ':', '헬로 월드']	# 공백기준, 3번 분할
```

## replace 함수
replace는 문자열을 변경하는 함수이다. 문자열 안에서 특정 문자를 새로운 문자로 변경하는 기능을 가지고 있다. 사용 방법은 '변수. replace(old, new, [count])' 형식으로 사용한다.
- old : 현재 문자열에서 변경하고 싶은 문자
- new: 새로 바꿀 문자
- count: 변경할 횟수. 횟수는 입력하지 않으면 old의 문자열 전체를 변경한다. 기본값은 전체를 의미하는 count=-1로 지정되어있다. 
replace(old, new, [count]) -> replace("찾을값", "바꿀값", [바꿀횟수])
#### 사용예시
```
>>> a = 'hello world'
>>> a.replace('hello','hi')
hi world
```

## 풀이
```python
def complex_number_multiply(a, b):
  a1 = int(a.split('+')[0])
  b1 = int(b.split('+')[0])

  a2 = int(a.split('+')[1].replace('i', ''))
  b2 = int(b.split('+')[1].replace('i', ''))
  return f'{(a1 * b1) + (a2 * b2)*(-1)}+{(a1 * b2) + (a2 * b1)}i' 
```
