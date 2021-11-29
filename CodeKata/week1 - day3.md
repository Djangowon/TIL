# 문제

String 형인 str 인자에서 중복되지 않은 알파벳으로 이루어진 제일 긴 단어의 길이를 반환해주세요.


```
str: 텍스트
return: 중복되지 않은 알파벳 길이 (숫자 반환)
```

예를 들어,

```
str = "abcabcabc"
return 은 3
=> 'abc' 가 제일 길기 때문
```

```
str = "aaaaa"
return 은 1
=> 'a' 가 제일 길기 때문
```

```
str = "sttrg"
return 은 3
=> 'trg' 가 제일 길기 때문
```

## 풀이
```python
def get_len_of_str(s):
    # 딕셔너리로 해싱
    longest = 0
    for i in range(len(s)):
      result = ' '
      count = 0
      for j in s[i:]:
        if j not in result:
          result +=j
          count +=1
        
        else:
          result =j
          count =1

        if count > longest:
          longest = count
    
    return longest
       
print(get_len_of_str('sttrg'))
```
