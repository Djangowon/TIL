# Django modeling
## User Branch 생성
```
$ git checkout main                      # 브랜치 생성은 꼭 main 에서 할 것
$ git checkout -b feature/dowon-models   # 브랜치 생성하면서 체크아웃 하는 방법 
```
## User App 생성
```
# 브랜치에서 작성할 것
python manage.py startapp 앱이름          # manage.py 가 위치한 곳에서 실행해야 함
```
## User table 생성
models.py 에 Model Class 작성을 통해 database  의 table 과 mapping  
#### models.py 작성 예시
```python
from django.db import models


class Menu(models.Model):
	name = models.CharField(max_length=20)
	
	class Meta:
		db_table = 'menus'

class Category(models.Model):
	name = models.CharField(max_length=20)
	menu = models.ForeignKey('Menu', on_delete=models.CASCADE)

    class Meta:
          db_table = 'categories'

class Product(models.Model):
	name     = models.CharField(max_length=100)
	category = models.ForeignKey('Category', on_delete=models.CASCADE)

	class Meta:
		db_table = 'products'
```
```python
from django.db import models

class User(models.Model):
	name         = models.CharField(max_length=45)
	email        = models.CharField(max_length=45, unique=True)
	password     = models.CharField(max_length=200)
	phone_number = models.CharField(max_length=45)
	information  = models.CharField(max_length=300, null=True)
	created_at   = models.DateTimeField(auto_now_add=True)
	updated_at   = models.DateTimeField(auto_now=True)

	class Meta:
		db_table = 'users'
```
#### models.py 작성 내용 DB에 적용
```
python manage.py makemigrations app이름
```
```
python manage.py migrate
```
