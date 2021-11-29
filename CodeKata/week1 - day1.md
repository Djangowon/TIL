# 문제

`two_sum`함수에 숫자 리스트와 '특정 수'를 인자로 넘기면, 더해서 '특정 수'가 나오는 index를 배열에 담아 return해 주세요.


```
nums: 숫자 배열
target: 두 수를 더해서 나올 수 있는 합계
return: 두 수의 index를 가진 숫자 배열
```

예를 들어,

```
nums은 [4, 9, 11, 14]
target은 13 

nums[0] + nums[1] = 4 + 9 = 13 이죠?

그러면 [0, 1]이 return 되어야 합니다.
```

# 가정

`target`으로 보내는 합계의 조합은 배열 전체 중에 `2`개 밖에 없다고 가정하겠습니다.

## 풀이
```python
def two_sum(nums, target):
    for i in range(len(nums)):
      for j in range(i+1, len(nums)):
        if nums[i] + nums[j] == target:
          return [i,j]
```
