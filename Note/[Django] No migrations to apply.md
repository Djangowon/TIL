# No migrations to apply
<img src="https://github.com/rosewoodowon/TIL/blob/main/image/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-11-14%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%2012.29.11.png/" width="80%" height="80%"/>
<img src="https://github.com/rosewoodowon/TIL/blob/main/image/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-11-14%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%2012.29.32.png/" width=70% height=70%/>
  
```
Operations to perform:
  Apply all migrations: contenttypes, products, sessions
Running migrations:
  No migrations to apply.
```
  
`models.py`를 수정하고 `0001_initial.py`를 지운 뒤, 다시 makemigrations 를 했을 때 정상적으로 테이블이 만들어진 것으로 떴지만 mysql 에서 테이블을 확인했을 때 일부 테이블만 생성되고 누락된 테이블들이 생겼다. migrate를 하면 위와 같은 `No migrations to apply.`가 떴다.
  
  
<img src="https://github.com/rosewoodowon/TIL/blob/main/image/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-11-14%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%201.02.58.png/" width=50% height=50%/>
DB의 django_migrations 테이블을 확인해보면 지금까지 migrate를 하면서 생성된 migration 파일 목록이 기록되어 있다. 동일한 App에 대해 migrate를 진행하면서 생성된 파일명이 이미 DB에 기록되어 있다면 Django는 해당 파일을 무시하고 아무 작업도 수행하지 않기 때문에, makemigrations 를 하고 생긴 `0001_initial.py` 파일의 파일명을 rename 한 후 migrate 를 하면 정상 동작하는 것처럼 보여지는데 이 또한 mysql 에서 테이블을 확인했더니 누락된 테이블 총 4개중 두개 테이블은 생성되었지만, 다른 누락된 테이블은 여전히 생기지 않았다. 뭐 때문에 이건 되고 저건 안 되는지 모르겠다. 아직 미해결. 
  
---
DB의 django_migrations 테이블을 확인해보면 지금까지 migrate를 하면서 생성된 migration 파일 목록이 기록되어 있다. 동일한 App에 대해 migrate를 진행하면서 생성된 파일명이 이미 DB에 기록되어 있다면 Django는 해당 파일을 무시하고 아무 작업도 수행하지 않는다.

이런 경우 생성된 파일명을 DB에 기록되지 않은 이름으로 변경한 후 migrate를 실행하면 된다.  
[참고자료](https://yungyikim-blog.tistory.com/entry/Django-%EB%B3%80%EA%B2%BD-%ED%95%AD%EB%AA%A9%EC%9D%B4-%EC%9E%88%EC%9D%8C%EC%97%90%EB%8F%84-migrate-%ED%96%88%EC%9D%84%EB%95%8C-No-migrations-to-apply%EC%9D%BC-%EA%B2%BD%EC%9A%B0/)
