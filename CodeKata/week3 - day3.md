# 문제
양수로 이루어진 m x n 그리드를 인자로 드립니다.
상단 왼쪽에서 시작하여, 하단 오른쪽까지 가는 길의 요소를 다 더했을 때,가장 작은 합을 찾아서 return 해주세요.

한 지점에서 우측이나 아래로만 이동할 수 있습니다.

Input:
[
&nbsp;&nbsp;  [1,3,1],
&nbsp;&nbsp;  [1,5,1],
&nbsp;&nbsp;  [4,2,1]
]

Output: 7

설명: 1→3→1→1→1 의 합이 제일 작음

## 풀이
```python
def min_path_sum(grid):

    m = len(grid)
    n = len(grid[0])
    
    ### 1
    for i in range(1, n):
        grid[0][i] += grid[0][i-1]
    for i in range(1, m):
        grid[i][0] += grid[i-1][0]
        
    ### 2
    for i in range(1, m):
        for j in range(1, n):
            grid[i][j] += min(grid[i-1][j], grid[i][j-1])
    return grid[-1][-1] 
```
