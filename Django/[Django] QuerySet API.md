# Django QuerySet API
쿼리셋(QuerySet)은 전달받은 모델의 객체 목록이고, 핵심은 Django에 내장 된 일반적인 데이터 관리 기능이다. 쿼리셋은 데이터베이스로부터 데이터를 읽고, 필터를 걸거나 정렬을 할 수 있다.

## 자주 사용되는 Model Method
`all()`,`filter()`,`exclude()`,`values()`,`values_list()`,`get()`,`create()`,`count()`,`exists()`,`update()`,`delete()`,`first()`,
`last()` . . .   

[공식문서](https://docs.djangoproject.com/en/3.2/ref/models/querysets/)

## QuerySet 반환되는 경우 vs.  반환되지 않는 경우
#### QuerySet 반환되는 경우
* all()
```python

```
