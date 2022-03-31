# Use alembic with existing database
## alembic을 사용해서 DB 마이그레이션 하는 방법
```
pip install alembic
```
```
alembic init `폴더 이름`   
```
작성한 폴더 이름으로 디렉토리가 생긴다.

<img src="https://github.com/Djangowon/TIL/blob/main/image/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-03-31%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%206.42.59.png" height=80% width=80%>

### alembic.ini
디렉토리와 함께 생성된 almebic.ini 파일 중반 쯤에 sqlalchemy.url 을 작성해줘야 한다.

```
# the output encoding used when revision files
# are written from script.py.mako
# output_encoding = utf-8

sqlalchemy.url = postgresql://%(DB_USER)s:%(DB_PASS)s@localhost/fastapi_store
```

### env.py
생성된 폴더 안에 env.py 안에 target_metadata 에 main 에 작성한 metadata 를 넣어준다.
++ 환경변수 추가하는 법
```
import os
from main import metadata


section = config.config_ini_section
config.set_section_option(section, "DB_USER", os.environ.get("USER"))
config.set_section_option(section, "DB_PASS", os.environ.get("PASSWORD"))


target_metadata = metadata
```

### 자동으로 alembic 버전 파일 만들기
```
alembic revision --autogenerate -m "Initial"
```
### migration 실행하기
버전 파일이 만들어지면 아래 명령어로 최신 버전 파일을 적용할 수 있다.
```
alembic upgrade head
```

<img src="https://github.com/Djangowon/TIL/blob/main/image/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-03-31%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%206.50.48.png" height=80% width=80%>

### show migration, 로그 확인하기
```
alembic history --verbose
```

