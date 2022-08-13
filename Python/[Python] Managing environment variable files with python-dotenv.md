# 환경변수란?

환경변수(environment variable)는 컴퓨터가 사용하는 동적인 변수를 의미한다. 여기서 동적이란 '고정적이지 않은'이라는 의미이다.

환경변수는 프로세스를 동작시키는 데 사용하는 변수를 매번 새로 입력할 필요 없이, 시스템에 설정해두어 사용하는 변수를 의미한다.

이번 글에서 Python 프로그램을 실행할 때 환경변수를 파일 단위로 관리할 수 있는 python-dotenv에 대해 알아보자.

<br><br>

# 환경변수 설정 방법

mac 기준, 환경 변수를 설정하는데 ‘임시 설정’과 ‘영구 설정’ 두 가지 방법이 있다.

<br>

### **임시 설정**

사용자가 터미널에 직접 환경 변수를 할당한다.

터미널에 export \[환경변수 이름\]=\[환경변수 값\] 형식으로 명령어를 입력해보자.

```
export environ=456
```

다시 export를 터미널에 입력하면 방금 입력한 환경변수 environ=456을 확인할 수 있다.

```
export
>>> environ=456
```

이 방법은 임시로 환경변수를 지정하는 방법으로 재부팅 후에는 환경변수가 초기화된다.

<br>

### **영구 설정**

두 번째 ‘영구 설정’ 방법은 환경변수를 문서에 미리 할당해두는 것이다.

zsh 터미널을 이용한다면 vi ~/.zshrc 명령어를 터미널에 입력해보자.

```
vi ~/.zshrc
```

아래 이미지처럼 vim으로 환경변수를 관리하는 문서가 열린다. (vim은 터미널 문서 편집기이다)

![image](https://blog.kakaocdn.net/dn/lc17E/btrJC4Lr1Qa/6DkKTLGxOLVoYgqHse7odk/img.png)

vim문법을 이용해 export environ=456을 입력하고 문서를 저장하면 456 값을 갖는 environ 환경변수를 만들 수 있다. 이 환경변수는 문서에 저장해두었으므로 지속적으로 사용할 수 있다.

<br>

두 가지 방법을 살펴보았지만 둘 다 불편하다.

<br>

매번 환경변수를 입력하거나 터미널 문서를 편집하지 않고, 프로젝트별로 편하게 환경변수를 관리할 수는 없는 걸까?

<br><br>

# python-dotenv

Python에서는 python-dotenv 라이브러리를 사용하여 환경변수를 쉽게 관리할 수 있다. 함께 사용법을 살펴보자.

우선 python-dotenv를 설치한다.

```
pip install python-dotenv
```

config.py 에서 .env 파일을 불러오기 위해 load\_dotenv를 import 한다.

```python
# config.py

from dotenv import load_dotenv

load_dotenv()
```

<br>

다음 .env 파일을 만든다. (파일명이 ‘. env’이다)

SECRET\_KEY라는 환경변수에 ‘덤벼라 세상아’라는 문구를 할당하겠다.

```python
# .env

SECRET_ENV=‘덤벼라 세상아’
```

<br>

다시 config.py 파일로 돌아와 os와 getenv 메서드를 통해 SECRET\_ENV 환경변수를 가져오자.

```python
import os
from dotenv import load_dotenv

load_dotenv()

SECRET_ENV = os.getenv("SECRET_ENV")
print(SECRET_ENV)
```

<br>
SECRET\_ENV = os.getenv("SECRET\_ENV")을 통해 .env 파일의 SECRET\_ENV 환경변수를 가져온다. 

print(SECRET\_ENV)로 환경변수를 잘 가져왔는지 출력해보자.

<br>

터미널에 python config.py 명령어로 파일을 실행해보면 ‘덤벼라 세상아’가 출력되는 것을 확인할 수 있다.

![Image](https://blog.kakaocdn.net/dn/b5qzRM/btrJCmSAgrQ/CSqY3IRdTzOEy3KKPBF8q1/img.png)

<br><br>

# 마무리

python-dotenv를 이용해 환경변수를 파일로 관리하는 방법을 알아보았다. 앞으로는 터미널을 이용하지 않고도 .env 파일을 통해 아래처럼 다양한 변수들을 설정할 수 있다.

```
SECRET_ENV=덤벼라 세상아
...
API_KEY=123
PASSWORD=456
ACCESS_TOKEN=789
...
```

python-dotenv을 이용하면 환경변수를 각 프로젝트별로 다르게 관리할 수 있다. 또한 동일 프로젝트에서도 일반 환경변수, 개발 환경변수 등을 각기 다르게 설정할 수 있다.

앞으로는 python-dotenv로 환경변수를 편하게 관리해보자!

<br>

### 주의할 점

보통 환경변수의 경우 중요하고 비밀스러운 정보를 담기 때문에 github이나 온라인상에 해당 환경변수들이 올라가지 않도록 주의해야 한다. 만약 비밀번호나 토큰 등이 외부에 유출될 경우 큰 피해를 입을 수 있으므로 주의하자!