# error: Your local changes to the following files would be overwritten by checkout: 
```
error: Your local changes to the following files would be overwritten by checkout: 
Please commit your changes or stash them before you switch branches. Aborting
```
여러 브랜치를 만들어놓고 작업을 하다가 다른 브랜치로 체크아웃을 할 때 만난 에러  
원인은 내 변경사항과 remote 변경사항의 충돌시 발생
pull 로 가져오려는 소스와 현재 저장된 코드가 제대로 처리가 되지 않아서 나는 에러이다.

#### 해결방법
내가 업데이트한 내용은 한켠에 제껴두고 remote repository로부터 최신상태로 변경해야 한다.
```
git stash
```
내가 수정한 소스를 스택 한켠에 옮겨두어 저장하고 이전 commit 시점으로 돌아간다.
이때 stash 는 현재 디렉토리의 파일을 임시로 백업하고 깨끗한 상태로 돌린다.
버전관리 되는 대상 파일들을 임시저장 해둔다고 보면 된다. 
 
#### 예방방법
* git status 로 항상 확인!

[참고](https://steemit.com/develope/@snowsprout/git-git-pull-error-your-local-changes-to-the-following-files-would-be-overwritten-by-merge/)  
