# git merge main Already up to date
main의 코드를 새로 생성한 브랜치로 병합하려 하는데 분명 main 코드가 변경되었음에도 불구하고 다음과 같은 에러가 떴다.
```
$ git merge main
Already up to date.
```
```
$ git pull origin main
```
이 때 merge가 아닌 Pull 명령어로 가져오면 가끔 해결이 된다.  
  
\+ git pull로 원격 저장소의 코드를 가져올 때에도 Already up to date 문구가 뜰 때
#### 해결방법
```
$ git fetch --all
```
```
$ git reset --hard origin/main
```
그럴 땐 위 명령어로 원격 저장소를 모두 fetch한 후 
해당 브랜치로 강제로 리셋시키면 된다는 정보를 알게 되었다.  
하지만 이 방법은 현재 로컬의 작업내역이 날라갈 수 있다는 위험성이 있다.  
[공식문서](https://stackoverflow.com/questions/25411366/git-repo-says-its-up-to-date-after-pull-but-files-are-not-updated/)  
[출처](https://wiselog.tistory.com/170/)
