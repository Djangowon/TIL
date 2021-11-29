# 문제
`nums`는 숫자로 이루어진 배열입니다.

가장 자주 등장한 숫자를 `k` 개수만큼 return 해주세요.  

```python
nums = [1,1,1,2,2,3],
k = 2

return [1,2]

nums = [1]
k = 1

return [1]
```

## 풀이
```python
def top_k(nums, k) :
    nums_set = set(nums)
    my_dict = {}
    result = []
    for i in nums_set :
        my_dict[nums.count(i)] = i  

    print(my_dict)
    my_dict = sorted(my_dict.items(), reverse=True)
    print(my_dict)

    for i in range(0,k) :
        result.append(my_dict[i][1])

    result.sort()
    return result


nums = [5,5,6]  
print(top_k(nums, 1))
```
