# Git revert & reset --hard, --mixed, --soft

## revert
revert는 특정 커밋을 골라서 없었던 일로 만든다. 특정 커밋을 없애주지만 revert를 했다는 이력이 남게 된다.  
지우려는 특정 커밋의 과거, 미래와 얽혀 충돌이 나는 경우가 많다.
```
git revert [COMMIT_ID]
```

## reset
특정 커밋으로 되돌아가게 되는데 과거로 되돌아갔으니 해당 커밋 이후의 커밋들은 모두 사라진다.  

## reset --hard
- repository, staging area, working directory의 모든 내용을 지정한 버전으로 reset한다.  
- 최근 작업 내용을 전부 버리고 최신 버전의 상태로 초기화 시키는 경우  
```
git reset --hard [COMMIT_ID]
```

## reset --mixed
- default 값. repository, staging area의 내용을 지정한 버전으로 reset한다. 작업한 내용을 다시 수정해서 commit할 때 좋다.  
- 최근 작업 내용도 살리고 최신 버전으로 돌아가서 add를 할지 말지 결정해야 하는 경우  
```
git reset --mixed [COMMIT_ID]
```

## reset --soft
- repository만 지정한 버전으로 reset한다. 지정한 버전에서 다음 버전으로 commit하기 직전 상태로 변경한다고 보면 좋겠다.  
- reset한 버전과 현재까지의 작업을 합쳐 새로운 버전을 만드는 경우  
- reset하기 전까지 했던 staging area, working directory의 작업은 남겨둠.
```
git reset --soft [COMMIT_ID]
```

[참고](https://www.atlassian.com/git/tutorials/undoing-changes/git-revert#:~:text=The%20git%20revert%20command%20is%20a%20forward%2Dmoving%20undo%20operation,in%20regards%20to%20losing%20work/)
