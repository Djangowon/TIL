# error: failed to push some refs to
```
> git add .
```
```
> git commit -m "커밋메세지 작성"
```
```
> git push origin feature/owner
```
commit 까지 한 뒤 push 를 했더니 만난 에러  
  
<img src="https://github.com/rosewoodowon/TIL/blob/main/image/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-11-16%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%203.41.11.png" width=70% height=70%>  
원인은 push하기 전 & 작업하기 전에 git pull 명령어를 통해서 원격저장소의 최신상태를 유지한 상태에서 push를 해야하는데 그냥 push 를 해서 생긴 것.

#### 해결방법
```
> git checkout main
```
```
> git pull origin main
```
```
> git checkout (서브)
```
```
> git merge main
```
```
> git push origin (서브)
```
push 하기 전에 main 에서 git pull 을 해주자!  

git pull 을 통해 원격 저장소를 로컬 저장소로 가져와 병합 후, 다시 push 하는 것이다.
pull 은 fetch (원격 저장소로부터 가져오기) 와 merge (서로 차이가 나는 부분을 조정해 병합하기) 가 합쳐진 것으로 한 번에 원격 저장소의 변경 내역을 현재 브랜치에 통합해준다.
그래도 push 에 계속 오류가 발생한다면, git push -f origin 을 통해 강제로 push 하는 방법이 있지만, 로컬과 원격의 충돌을 무시하고 진행하기 때문에 레포지토리를 날려버리게 될 수도 있으니 주의.
```
> git push -f origin (서브)
```
