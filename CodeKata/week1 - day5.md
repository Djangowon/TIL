# 문제

strs은 단어가 담긴 배열입니다.

공통된 시작 단어(prefix)를 반환해주세요.  

예를 들어

```
strs = ['start', 'stair', 'step']
return은 'st'
```

```
strs = ['start', 'wework', 'today']
return은 ''
```
## sorted 함수
sorted 함수는 파이썬 내장 함수로, 첫 번째 매개변수로 들어온 이터러블한 데이터를 새로운 정렬된 리스트로 만들어서 반환해 주는 함수이다.
- 첫 번째 매개변수로 들어올 "정렬할 데이터"는 iterable 한 데이터 이어야 한다.

아래 옵션(파라미터)은 다 기본값으로 들어가 있기 때문에 sorted(정렬 데이터)만 넣어도 충분하다.

- key 옵션 (key 파라미터)
sorted 함수의 key 파라미터는 어떤 것을 기준으로 정렬할 것인가? 에 대한 기준이다.
즉, key 값을 기준으로 비교를 하여 정렬을 하겠다는 것인데, 이것을 정해 줄 수 있는 파라미터이다.
sorted( ~~ , key=뭐뭐)로 입력하게 되면 해당 키를 기준으로 정렬하여 반환한다.

- reverse 옵션 (reverse 파라미터)
해당 파라미터를 이용하면 오름차순으로 정렬할지 내림차순으로 정렬할지 정할 수 있다.
디폴트로는 reverse=False로 오름차순으로 정렬이 된다.
sorted( ~~ , reverse=True)로 입력하게 되면 내림차순으로 정렬하여 반환한다.

** 리스트.sort()와 sorted(리스트)의 가장 큰 차이는
리스트.sort() 는 본체의 리스트를 정렬해서 변환하는 것이고,
sorted(리스트) 는 본체 리스트는 내버려두고, 정렬한 새로운 리스트를 반환하는 것이다.  
[출처](https://blockdmask.tistory.com/466/)

## startswith, endswith 메서드
파이썬 startswith () 메서드는 주어진 문자열의 시작, 끝을 판단하여 조건을 만족하면 True, 만족하지 않으면 False를 반환하는 메서드이다.  


## 풀이
```python
def get_prefix(strs):
    if len(strs) == 0:
        return '' 
    res = ''
    strs = sorted(strs)
    for i in strs[0]:
        if strs[-1].startswith(res+i):
            res += i
        else:
            break
    return res
```
우선 처음에 strs의 길이가 0일 경우 비어있는 배열이므로 ''을 리턴하고, 빈 result 변수를 만들어준 뒤 sorted 함수로 strs 배열을 정렬시켜준다.  
예제처럼 strs = ['start', 'stair', 'step'] 일 경우로 예를 들어보면, sorted(strs) 로 정렬시켰을 때 ['stair', 'start', 'step'] 이렇게 된다.  
이제 sorted로 정렬을 시켰기 때문에 정렬된 단어 배열에서 첫번째 단어와 마지막 단어만 비교하면 된다.  
startswith 메서드를 이용하여 '만약 i 가 strs의 [0] 번째 인덱스 안에 있다면(첫번째 단어라면), strs의 [-1] 번째 인덱스(마지막 단어)가 res + i 로 시작하는지' 조건을 걸어준다.  
처음에는 res 가 빈 변수이지만 이제 + i 가 되어 res + i ('' + s) 가 되는 것이고, 한번 더 for문이 실행되어서 i 가 strs의 첫번째 단어에 있다면 마지막 단어 문자열의 시작이 i 이므로 res + i (s + t)가 된다.  
그 다음에 이제 i = a 일 때 for문이 실행되면 마지막 단어의 시작은 ( s + t + i(a) )가 아니므로 else가 되고 break, i(a)를 제외한 st 만 반환하게 된다.
