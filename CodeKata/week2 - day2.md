# 문제

숫자로 이루어진 배열인 nums를 인자로 전달합니다.

숫자중에서 과반수(majority, more than a half)가 넘은 숫자를 반환해주세요. 

예를 들어, 
```python
nums = [3,2,3]
return 3

nums = [2,2,1,1,1,2,2]
return 2
```

# 가정
`nums` 배열의 길이는 무조건 `2` 이상입니다.
## 풀이
```python
def more_than_half(nums):
   
    majority = len(nums) / 2 
    nums_set = set(nums)
    #print(nums_set)
    for i in nums_set:
      #print(nums.count(i))
      if majority < nums.count(i):
        return i

nums = [3,2,3,2,3,3,3,3]
print(more_than_half(nums))
  
```
