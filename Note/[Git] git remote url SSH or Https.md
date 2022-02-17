# git remote url SSH or Https
## Git 주소 확인하기(https or ssh 연결 확인)
* GitHub에서 https 와 ssh 프로토콜 2개를 모두 지원한다.
* 이 때, git URL 도 다른 방식으로 저장되고,  URL이 ssh 또는 http에 따라서 ID와 Password 인증 방식이 다르기 때문에 각각 맞는 방법으로 설정해야 함
* Git clone 시 SSH URL로 만든 경우라면 Public key를 GitHub 사이트에 등록해야 사용할 수 있다. 
    * 하지만, 회사 방화벽에서 ssh 연결을 막아 놓은 상태라면 https 연결을 사용해야 함
    * 이 경우 ID에 맞는 ACCESS Token을 할당받아서 git clone 시  URL에 설정하거나, 또는 git crendential cache를 활용할 수 있다.
    

## https와 ssh 전환하기
#### (Https로 만든 경우) $ git remote -v
```
origin  https://github.com/Djangowon/branch.git (fetch)
origin  https://github.com/Djangowon/branch.git (push)
```
#### (SSH로 만든 경우) $ git remote -v
```
origin  git@github.com:Djangowon/branch.git (fetch)
origin  git@github.com:Djangowon/branch.git (push)
```

#### (https에서 ssh URL로 전환)
```
$ git remote set-url oprigin git@github.com:Djangowon/branch.git
```
#### (ssh에서 https URL로 전환)
```
$ git remote set-url oprigin git@github.com:Djangowon/branch.git
```
