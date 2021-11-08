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
## Absolute Path & Relative Path
파이썬의 built-in 모듈과 pip 을 통해 설치한 외부 모듈 및 package는 일반적으로 import 하는데 큰 문제가 되지 않는다. Built-in 모듈은 당연히 잘 찾아지고, pip 으로 설치한 외무 모듈도 자동으로 site-packages 라는 디렉토리에 설치가 되는데, 이 site-packages 는 sys.path에 이미 포함되어 있기때문에 찾는데 문제가 없다. 문제는 직접 개발한 local package 이다. 직접 개발한 local package를 import 할때는 해당 package의 위치에 맞게 import 경로를 잘 선언해야 한다.
Local package를 import 하는 경로에는 absolute path 와 relative path 가 있다. Absolute path는 이름 그대로 절대 경로이다. 왜 절대 경로인가 하니, import를 하는 파일이나 경로에 상관없이 항상 경로가 동일하기 때문이다.

다음과 같은 프로젝트를 예를 들어보자:
```
└── my_app
    ├── main.py
    ├── package1
    │   ├── module1.py
    │   └── module2.py
    └── package2
        ├── __init__.py
        ├── module3.py
        ├── module4.py
        └── subpackage1
            └── module5.py
```
my_app 이라는 프로젝트 이며 package1과 package2 라는 2개의 package를 가지고 있다.  
그리고 package2는 subpackage2 라는 중첩 package를 가지고 있다.  
Absolute path를 사용해 package1 과 package2를 import 하면 다음과 같다.  
```python
from package1 import module1
from package1.module2 import function1
from package2 import class1
from package2.subpackage1.module5 import function2
```
경로들의 시작점이 전부 my_app 프로젝트의 가장 최상위 디렉토리에서 시작하는것을 볼 수 있다. 예를 들어, subpackage1의 module5 모듈의 function2 함수를 import 하기 위해서는 다음 경로를 거치게 된다.
```
my_app => package2 => subpackage1 => module5.py
```
이걸 리눅스의 directory 경로 형식으로 바꾸면 다음처럼 표현 할 수 있다.
```
my_app/package2/subpackage1/module5.py
```
윈도우스 형식이라면 다음과 같다.
```
my_app/package2/subpackage1/module5.py
```
파이썬에서는 slash나 back slash대신에 dot .을 사용해서 경로를 표현한다.
```
my_app.package2.subpackage1.module5.py
```
이미 my_app 프로젝트 안에 있으므로 my_app 은 생략된다. 그러므로 다음처럼 경로를 표현하게 되는 것이다.
```
package2.subpackage1.module5.py
```
이걸 from import 키워드를 사용해 import 하게 되면 다음 처럼 된다.
```
from package2.subpackage1.module5 import function2
```
my_app 프로젝트 내에서는 어느 파일, 어느 위치에서 import 하던지 경로가 항상 위와 같이 동일하게 되므로 absolute path 라고 하는 것이다.  
참고로 current directory 라고 하는 현재의 프로젝트 디렉토리는 default로 sys.path 에 포함되게 된다.  
그러므로 absolute path는 current directory 로 부터 경로를 시작하게 되는 것이다.  
일반적으로 local package를 import 할때는 absolute path를 사용하면 된다.  
다만 absolute path를 사용하게 되면 한가지 단점이 있는데 바로 경로가 길어질 수 있다는 점이다.  
그래서 이러한 단점을 보완하기 위해서 relative path를 사용할 수 있다.  
Relative path 는 absolute path와 다르게 프로젝트의 최상단 디렉토리를 기준으로 경로를 잡는게 아니라 import 하는 위치를 기준으로 경로를 정의한다. 
그래서 일반적으로 relative path는 local package 안에서 다른 local package를 import 할때 사용된다.  
예를 들어, package2의 module3에서 package2의 class1과 package2의 하위 package인 subpackage1의 module5의 function2 함수를 import 하려고 하면 다음 처럼 할 수 있다.
```python
# package2/module3.py

from . import class1
from .subpackage1.module5 import function2
```
여기서 dot .은 import 가 선언되는 파일의 현재 위치를 이야기 한다.  
현재위치는 package2/module3.py 이므로 현재 위치에서부터 원하는 모듈의 경로만 선언해주면 되는 것이다.  
또한 dot 2개를 사용할 수도 있다. dot 2개 .. 는 현재위치에서 상위 디렉토리로 가는 경로이다.  
```python
# subpackage1/module5.py
from ..module4 import class4
```
Relative path는 선언해야 하는 경로의 길이를 줄여준다는 장점은 있지만 헷갈리기 쉽고 파일 위치가 변경되면 경로 위치도 변경되어야 하는 단점이 있다.
그러므로 웬만한 경우 absolute path를 사용하는게 권장된다.
