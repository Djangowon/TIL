# * 문제

reverse 함수에 정수인 숫자를 인자로 받습니다.

그 숫자를 뒤집어서 return해주세요.

x: 숫자

return: 뒤집어진 숫자를 반환!

예들 들어,

```
x: 1234
return: 4321
```

```
x: -1234
return: -4321
```

```
x: 1230
return: 321
```

## 풀이
```python
def reverse(number):
 
    if number > 0:
        a = str(number)
        a_reverse = a[::-1]
        return int(a_reverse)
    elif number == 0:
        return 0
    elif number < 0:
        b = str(abs(number))
        b_reverse = int(b[::-1])
        return b_reverse * -1      
```
```python
y = str(abs(number))

    y = y[::-1]
    output = int(y)
    if number < 0 :
        return -1 * output
    else:
        return output
```
