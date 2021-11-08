# sys.module & sys.path
Python은 여러 모듈이 합쳐져서 프로젝트를 이루게 된다 pip를 이용하여 모듈 패키지를 추가할 수 있고 용도에 따라 웹개발이나, AI/ML개발, 게임 개발 등이 가능하다. 개발자 개인이 만든 local package module 을 이용하여 더 다양한 프로젝트를 만들 수 있다. import를 써서 모듈과 패키지를 찾는다.  
#### import search order
Python은 크게 세가지 구역에서 아래와 같은 순서로 module/package들을 찾게 된다.
```
sys.modules => built-in modules => sys.path
```

## sys.module
파이썬이 모듈이나 package를 찾기위해 가장 먼저 확인하는 곳이다.
sys.modules는 단순한 dictionary 이며, 이미 import된 모듈과 package들을 저장하고 있다.
즉, 한번 import된 모듈과 Package들은 파이썬이 또 다시 찾지 않아도 되도록 하는 기능을 가지고 있다.
그러므로 새로 import하는 모듈은 sys.modules에서 찾을 수 없다.
sys 모듈은 Python 런타임 환경의 다른 부분을 조작하는 데 사용되는 함수와 변수를 제공한다.
* 파이썬이 가장 먼저 모듈이나 패키지를 찾는 곳
* dictionary 구조
* import 되어있는 모듈과 패키지를 저장(한번 import 하면 또 다시 import하지 않아도 됨)
## built-in modules
파이썬에서 공식으로 제공하는 라이브러리이다. 당연히 설치하자 마자 깔리는 것들이고 쉽게 찾을 수 있게 된다. sys.modules print() 출력 결과를 확인하게 되면 어떤 것이 built-in modules인지 쉽게 확인 할 수 있다.  
## sys.path
파이썬이 module이나 package를 찾을 때 가장 마지막으로 확인하는 부분이다. pip로 새롭게 설치한 패키지도 이 곳을 통해 찾게 되며 새롭게 작성한 패키지나 모듈을 사용하고자 할 때 이 곳에 path를 등록 해서 찾게끔 설정해 준다.(설정하는 방법은 해당 시스템의 OS에 따라 다소 차이가 있다) sys.path는 기본적으로 list이며 string 요소들을 가지고 있는 list이다.(쉽게 할당 삭제가 가능하다)
각 string 요소들은 다음 처럼 경로를 나타낸다.
* 모듈과 패키지를 1,2번째로 찾고 마지막으로 sys.path를 찾음
* 리스트 구조(string 요소)
* 처음의 리스트 요소부터 마지막까지 찾음
* 파이썬에 포함되어 있는 built-in-modules
* sys.path에서도 모듈을 발견하지 못하면 ModuleNotFoundError 에러를 리턴한다.
