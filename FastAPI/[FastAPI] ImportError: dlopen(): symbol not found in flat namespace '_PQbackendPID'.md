# ImportError: dlopen(): symbol not found in flat namespace '_PQbackendPID'

```
alembic revision --autogenerate -m "Initial migration"   
```
위의 명령어로 DB 마이그레이션을 할 때 다음과 같은 에러를 만났다.

<img src="https://github.com/Djangowon/TIL/blob/main/image/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-04-01%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%203.29.08.png" height=100% width=100%>

```
Traceback (most recent call last):
  File "/Users/jangdowon/.local/share/virtualenvs/clothes-xL1mbFXc/bin/alembic", line 8, in <module>
    sys.exit(main())
  File "/Users/jangdowon/.local/share/virtualenvs/clothes-xL1mbFXc/lib/python3.9/site-packages/alembic/config.py", line 588, in main
    CommandLine(prog=prog).main(argv=argv)
  File "/Users/jangdowon/.local/share/virtualenvs/clothes-xL1mbFXc/lib/python3.9/site-packages/alembic/config.py", line 582, in main
    self.run_cmd(cfg, options)
  File "/Users/jangdowon/.local/share/virtualenvs/clothes-xL1mbFXc/lib/python3.9/site-packages/alembic/config.py", line 559, in run_cmd
    fn(
  File "/Users/jangdowon/.local/share/virtualenvs/clothes-xL1mbFXc/lib/python3.9/site-packages/alembic/command.py", line 227, in revision
    script_directory.run_env()
  File "/Users/jangdowon/.local/share/virtualenvs/clothes-xL1mbFXc/lib/python3.9/site-packages/alembic/script/base.py", line 563, in run_env
    util.load_python_file(self.dir, "env.py")
  File "/Users/jangdowon/.local/share/virtualenvs/clothes-xL1mbFXc/lib/python3.9/site-packages/alembic/util/pyfiles.py", line 92, in load_python_file
    module = load_module_py(module_id, path)
  File "/Users/jangdowon/.local/share/virtualenvs/clothes-xL1mbFXc/lib/python3.9/site-packages/alembic/util/pyfiles.py", line 108, in load_module_py
    spec.loader.exec_module(module)  # type: ignore
  File "<frozen importlib._bootstrap_external>", line 850, in exec_module
  File "<frozen importlib._bootstrap>", line 228, in _call_with_frames_removed
  File "migrations/env.py", line 79, in <module>
    run_migrations_online()
  File "migrations/env.py", line 61, in run_migrations_online
    connectable = engine_from_config(
  File "/Users/jangdowon/.local/share/virtualenvs/clothes-xL1mbFXc/lib/python3.9/site-packages/sqlalchemy/engine/create.py", line 755, in engine_from_config
    return create_engine(url, **options)
  File "<string>", line 2, in create_engine
  File "/Users/jangdowon/.local/share/virtualenvs/clothes-xL1mbFXc/lib/python3.9/site-packages/sqlalchemy/util/deprecations.py", line 309, in warned
    return fn(*args, **kwargs)
  File "/Users/jangdowon/.local/share/virtualenvs/clothes-xL1mbFXc/lib/python3.9/site-packages/sqlalchemy/engine/create.py", line 560, in create_engine
    dbapi = dialect_cls.dbapi(**dbapi_args)
  File "/Users/jangdowon/.local/share/virtualenvs/clothes-xL1mbFXc/lib/python3.9/site-packages/sqlalchemy/dialects/postgresql/psycopg2.py", line 782, in dbapi
    import psycopg2
  File "/Users/jangdowon/.local/share/virtualenvs/clothes-xL1mbFXc/lib/python3.9/site-packages/psycopg2/__init__.py", line 51, in <module>
    from psycopg2._psycopg import (                     # noqa
ImportError: dlopen(/Users/jangdowon/.local/share/virtualenvs/clothes-xL1mbFXc/lib/python3.9/site-packages/psycopg2/_psycopg.cpython-39-darwin.so, 0x0002): symbol not found in flat namespace '_PQbackendPID'

```

psycopg2-binary 는 이미 인스톨 되어있는데 왜지? 
```
pip install psycopg2-binary
```
위의 명령어로 설치하면 계속 같은 에러가 뜸

찾아본 결과 M1 이슈가 있는 것 같다.

## 해결방법
psycopg2-binary 를 제거했다가 다시 설치하는데, 캐시를 사용하지 않도록 설정해주어야 한다.

```
pip3.9 install psycopg2-binary --force-reinstall --no-cache-dir
```

<img src="https://github.com/Djangowon/TIL/blob/main/image/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-04-01%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%203.35.10.png" height=100% width=100%>

[Ref](https://stackoverflow.com/questions/65059310/apple-m1-install-psycopg2-package-symbol-not-found-pqbackendpid)
