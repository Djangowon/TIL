# delete `__pycache__`
## __pycache__란?
* Python은 인터프리터 언어이기 때문에 바이트 코드를 컴파일 하고 __pycache__ 폴더에 저장한다. 
* 거기에서 보면 프로젝트 폴더에 .py 파일 이름을 공유하는 많은 파일이 있으며 확장자는 `.pyc` 또는 `.pyo`이다. 
* 이들은 각각 바이트 코드 컴파일 및 최적화 된 바이트 코드 컴파일 버전의 프로그램 파일이다. 
* 역할은 좀 더 프로그램을 빠르게 시작하게 만들어주기 위해 만들어졌다. 
* 스크립트가 변경되면 다시 컴파일되고 파일이나 전체 폴더를 삭제하고 프로그램을 다시 실행하면 해당 동작이 특별히 억제되지 않는 한 다시 생성된다.

</br>

## 1) 아직 push하지 않은 경우
### .gitignore
```
# Byte-compiled / optimized / DLL files
__pycache__/
*.py[cod]
```
.gitignore에 위처럼 이미 적어주었는데도 레포에 생성되는 경우가 종종 있었다.


</br>

## 2) gitignore 추가 전에 이미 push하여 반영된 경우
아래 명령어를 실행하면 해당 이름을 갖는 모든 파일들이 강제로 제거된다.
```
find . -name "*.pyc" -exec git rm {} \;
```
```
git ls-files '*.pyc' | xargs git rm -f
```

</br>

[Ref](https://potato-potahto.tistory.com/180)
