# git stash
현재 stage에 있는 파일(add하기 전 현재 수정중인 파일)들을 임시적으로 저장해 둘 수 있다.

저장하기
```
git stash
```

저장하기 - save
```
git stash save [description]
description 추가   ex) git stash save '설명추가'
```

목록보기 - list
```
git stash list
```
적용하기 - apply 적용 후에도 리스트에 유지
```
git stash apply
가장 최근의 stash내용이 적용된다
```
```
git stash apply stash@{숫자}
원하는 저장이력 적용   ex) git stash apply 2
```
적용하기 - pop 적용 후 리스트에서 삭제
```
git stash pop
가장 최근의 stash내용이 적용되고 삭제된다
```
```
git stash pop stash@{숫자}
원하는 저장이력 적용    ex) git stash pop 2
```
삭제하기 - drop 적용 후 리스트에서 삭제
```
git stash drop
가장 최근의 stash내용이 삭제된다
```
```
git stash drop stash@{숫자}
원하는 저장이력 삭제    ex) git stash drop 3
```
전체삭제 - clear
```
git stash clear
```
적용내용 브런치로 가져오기
```
git stash branch [새로만들 브런치이름] stash@{숫자}
stash내용으로 브런치가 생성되고 생성된 브런치로 checkout되며 stash는 삭제된다
```
