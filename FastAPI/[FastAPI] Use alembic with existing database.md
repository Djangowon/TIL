# Use alembic with existing database
## alembic을 사용해서 DB 마이그레이션 하는 방법
```
pip install alembic
```

<br>

```
alembic init `폴더 이름`   
```

<br>
작성한 폴더 이름으로 디렉토리가 생긴다.<br>
<br>


<img src="https://github.com/Djangowon/TIL/blob/main/image/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-03-31%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%206.42.59.png" height=80% width=80%>

<br>
<br>

### alembic.ini

디렉토리와 함께 생성된 alembic.ini 파일 중반 쯤에 sqlalchemy.url 을 작성해줘야 한다.

```
# the output encoding used when revision files
# are written from script.py.mako
# output_encoding = utf-8

sqlalchemy.url = postgresql://%(DB_USER)s:%(DB_PASS)s@localhost/fastapi_store
```

위에 기재된 DB_USER, DB_PASS 는 환경변수이다.<br>
해당 파일에서 환경변수를 적용하려면 env.py에 코드를 추가해야한다.<br>
<br>
<br>

### env.py

생성된 폴더 안에 env.py 파일을 열어보자.<br>
main 에 작성한 metadata 를 import 하여 'target_metadata' 변수에 넣어준다.<br>

++ <br>
그리고 위에 언급한 환경변수 코드를 추가하자.<br>

```
import os
from main import metadata

target_metadata = metadata


# 아래 코드는 alembic.ini 에서 환경변수가 적용될 수 있도록 해준다.
section = config.config_ini_section
config.set_section_option(section, "DB_USER", os.environ.get("USER"))
config.set_section_option(section, "DB_PASS", os.environ.get("PASSWORD"))

```
main의 'metadata'에 대해 궁금하다면 다음 레포를 참고하라. <br>
[repo-link](https://github.com/Djangowon/fastapi-store/blob/main/main.py)

<br>
<br>

### 자동으로 alembic 버전 파일 만들기
```
alembic revision --autogenerate -m "Initial"
```
versions 폴더 안에 migration 버전 파일이 자동 생성된다. 

<br>
<br>

### migration 실행하기
버전 파일이 만들어지면 아래 명령어로 최신 버전 파일을 적용할 수 있다.
```
alembic upgrade head
```

<img src="https://github.com/Djangowon/TIL/blob/main/image/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-03-31%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%206.50.48.png" height=80% width=80%>

<br>
<br>

### migration 되돌리기
만약 다시 되돌리고 싶다면 아래 명령어로 롤백할 수 있다. <br>
(지정한 음수 만큼 버전 수를 되돌릴 수 있음) <br>
```
alembic downgrade -1    # -1 은 직전 버전으로 되돌린다.
```

upgrade와 downgrade의 내용은 각 버전 파일에 명시되어 있으므로 확인 후 migration하는 것을 권장한다.




<br>
<br>

### show migration, 로그 확인하기
```
alembic history --verbose
```

<br>
<br>


### tree 구조 예시
```
.
├── README.md
├── app
├── alembic.ini
└── migrations
    ├── README
    ├── env.py
    ├── script.py.mako
    └── versions
        └── Initial.py
```
