# Commit message rules
## 7 rules
1. 제목과 본문을 빈 행으로 구분합니다.
2. 제목을 50글자 이내로 제한합니다.
3. 제목의 첫 글자는 대문자로 작성합니다.
4. 제목의 끝에는 마침표를 넣지 않습니다.
5. 제목은 명령문으로! 과거형을 사용하지 않습니다.
6. 본문의 각 행은 72글자 내로 제한합니다.
7. 어떻게 보다는 무엇과 왜를 설명합니다.
## commit message 구조
```python
$ <type>(<scope>): 
<subject>       -- 헤더 
<BLANK LINE>    -- 빈 줄 
<body>          -- 본문 
<BLANK LINE>    -- 빈 줄 
<footer>.       -- 바닥 글
```
### <type>
```
feat : 새로운 기능에 대한 커밋 
fix : build 빌드 관련 파일 수정에 대한 커밋 
build : 빌드 관련 파일 수정에 대한 커밋 
chore : 그 외 자잘한 수정에 대한 커밋(rlxk qusrud) 
ci : CI 관련 설정 수정에 대한 커밋 
docs : 문서 수정에 대한 커밋 
style : 코드 스타일 혹은 포맷 등에 관한 커밋 
refactor : 코드 리팩토링에 대한 커밋 
test : 테스트 코드 수정에 대한 커밋
```
[출처](https://beomseok95.tistory.com/328/)
