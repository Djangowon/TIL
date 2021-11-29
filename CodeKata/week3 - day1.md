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
#### 사용예시
```python
text = '123,456,789,999'

replaceAll= text.replace(",","")
replace_t1 = text.replace(",", "",1)
replace_t2 = text.replace(",", "",2)
replace_t3 = text.replace(",", "",3)
print("결과 :")
print(replaceAll)
print(replace_t1)
print(replace_t2)
print(replace_t3)

'''
결과 : 
123456789999
123456,789,999
123456789,999
123456789999
'''
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
