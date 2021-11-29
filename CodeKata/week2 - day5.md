# 문제
인자인 height는 숫자로 이루어진 배열입니다.그래프로 생각한다면 y축의 값이고, 
높이 값을 갖고 있습니다. 

아래의 그래프라면 height 배열은 [1, 8, 6, 2, 5, 4, 8, 3, 7] 입니다.

![Graph](https://storage.googleapis.com/replit/images/1555380144403_97221ca23fbb92beaae5b6c800ceb5c8.pn)

저 그래프에 물을 담는다고 생각하고, 물을 담을 수 있는 가장 넓은 면적의 값을 반환해주세요.  
# 가정
배열의 길이는 2이상입니다.

## 풀이
```python
def get_max_area(height):
  area = 0
  for start in range(len(height)):
    for end in range(len(height)-1, start, -1):
      min_height = min(height[start], height[end])
      area = max(min_height * (end-start), area)
  return area
```
