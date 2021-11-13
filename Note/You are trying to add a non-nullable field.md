# You are trying to add a non-nullable field
models.py 를 수정한 뒤에 makemigrations 를 했더니 다음과 같은 오류를 만났다.   
```
You are trying to add a non-nullable field 'nutrition' to product without a default; we can't do that (the database needs something to populate existing rows).
Please select a fix:
 1) Provide a one-off default now (will be set on all existing rows with a null value for this column)
 2) Quit, and let me add a default in models.py
```
정확히 말하자면 에러는 아니고 기존에 makemigrations 를 통해 존재하는 정보들을 어떻게 수정할 지 정하지 않았기 때문에 나오는 메세지라고 보면 된다.  
즉, 기존 모델링으로 데이터베이스 내 테이블들이 생성되었고 모델링이 바뀐걸 적용하려니 빈 공간들이 생겼는데 그걸 어떻게 할 지 물어보는 것이다. 
구글링 결과 해당 필드 속성에 `null=True` 를 추가해주거나, 필드의 default 값을 설정하면 된다고 하여 `default=0`을 주었다.
```python
class Nutrition(models.Model):
    kcal = models.DecimalField(max_digits=5, decimal_places=2, default=0)
    sodium = models.DecimalField(max_digits=5, decimal_places=2, default=0)
    fat = models.DecimalField(max_digits=5, decimal_places=2, default=0)
    sugar = models.DecimalField(max_digits=5, decimal_places=2, default=0)
    protein = models.DecimalField(max_digits=5, decimal_places=2, default=0)
    caffeine = models.DecimalField(max_digits=5, decimal_places=2, default=0)
    class Meta:
        db_table = "nutritions"
```
`default=0` 과 `null=True` 를 같이 추가하는 경우에도 충돌이 날 수도 있다.  
이렇게 수정한 후에도 makemigrations 를 했더니 같은 메세지가 나왔는데, 이 때는 makemigrations 를 하면 생성되는 0001_initial.py, 0002~로 시작되는 모듈들을 삭제하고 makemigrations 를 하면 해결된다.

```
cd migrations
``` 
```
la
```
로 목록 확인 후, 나의 경우 0001_initial.py 하나가 있어서 삭제해주었다. 
```
rm 0001_initial.py
```
이렇게 되면 migrations 에는 `__init__.py` 와 `__pycache__` 만 남아있을 것이고, 이제 `python manage.py makemigrations`를 하면 정상적으로 잘 된다.
