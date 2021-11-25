# Django View
## models.py 작성 이후 views.py 작성하기
#### views.py
```python 
import json

from django.http     import JsonResponse
from django.views    import View

from products.models import Menu, Category, Product

class ProductsView(View):
    def post(self, request):
		    data     = json.loads(request.body)
        menu     = Menu.objects.create(name=data['menu'])
        category = Category.objects.create(
                name = data['category'],
                menu = menu
        )
        Product.objects.create(
                name     = data['product'], 
                category = category,
								menu     = menu
        )
        return JsonResponse({'MESSAGE':'CREATED'}, status=201)
```
View 를 작성 한 후에는, 클라이언트의 요청을 받아 적절한 view 를 맵핑해주는 urls.py 를 작성해주어야 한다.
