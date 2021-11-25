# Django View
## models.py 작성 이후 views.py 작성하기 (예시: westagram)
#### views.py
```python 
import json, bcrypt, jwt

from django.views           import View
from django.http            import JsonResponse, HttpResponse
from django.core.exceptions import ValidationError

from .models                import User
from my_settings            import SECRET_KEY, DATABASES, ALGORITHM
from .validation            import validate_email, validate_password

class SignupView(View):
    def post(self, request):
        try:
            data = json.loads(request.body)

            name         = data['name']
            email        = data['email']
            password     = data['password']
            phone_number = data['phone_number']
            information  = data.get('information', None)

            if User.objects.filter(email=email).exists():
                raise ValidationError('ALREADY_EXISTS')
            
            validate_email(email)
            validate_password(password)

            hashed_password = bcrypt.hashpw(password.encode('utf-8'), bcrypt.gensalt()).decode('utf-8')

            User.objects.create(
                name         = name, 
                email        = email, 
                password     = hashed_password, 
                phone_number = phone_number,
                information  = information
            )
            return JsonResponse({'message' : 'SUCCESS!'}, status=201)

        except KeyError:
            return JsonResponse({'message' : 'KEY_ERROR'}, status=400)

```
View 를 작성 한 후에는, 클라이언트의 요청을 받아 적절한 view 를 맵핑해주는 urls.py 를 작성해주어야 한다.  
메인 urls.py 말고 앱이름으로 생성된 디렉토리 안에는 urls.py 가 없는 게 맞고 생성해주어야 함
```
touch urls.py
vi urls.py
```
#### 앱이름/urls.py
```python
from django.urls import path
from .views      import SignupView, SigninView

urlpatterns = [
    path('/signup', SignupView.as_view()),
    path('/signin', SigninView.as_view()),
]
```
#### main/urls.py
```
from django.urls import path, include

urlpatterns = [
    path('users', include('users.urls')),
]
```
## httpie(client) 로 django server 에 요청보내기 (예시: westarbucks)
```
$ http -v POST 127.0.0.1:8000/product menu='음료' category='콜드브루' 
product='맛있는 콜드브루'
```
```
$ http -v GET 127.0.0.1:8000/products
```
