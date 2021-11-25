# Python Coding Convention
나 혼자 이해할 수 있는 코드는 좋은 코드가 아니다. 다른 개발자들도 쉽게 이해할 수 있는 코드를 쓰자.
* 깔끔한 코딩 스타일
* 간단하고 명료한 로직
* 명확한 변수, 함수, 클래스 등의 이름
## Naming
변수, 함수, 클래스, 모듈, 패키지 등의 이름은 한 눈에 그 목적을 이해할 수 있는 이름을 선택한다. 이름만 보더라도 목적이나 기능이 파악되어야 하고 몇 만줄의 코드가 되었을 때 다른 개발자가 보았을 때도 리네임하지 않도록 명확한 이름을 선정해줄 것. 
|Name|Convention|예시|
|:---|:---|:---|
|변수 (variable)|소문자만 사용하며 `_`를 사용하여 단어들을 구분. 명사로만 구성.|`user`,`users`,`total_cost`|
|상수 (constant)|대문자만 사용하며 `_`를 사용하여 단어들을 구분. 명사로만 구성.|`DEBUG_LEVEL`,`MAX_USERS`,`VIP`|
|함수 (function)|소문자만 사용하며 `_`를 사용하여 단어들을 구분. 동사를 사용하여 이름 구성.|`get_users`.`calculate_total_cost`|
|클래스 (class)|대문자와 소문자 둘 다 사용. 다만 대문자는 단어들을 구분하는 용도로 단어들의 첫글자만 대문자 사용. 명사로만 구성.|`User`,`HttpRequest`|
|모듈 (module)|소문자만 사용하며 `_`를 사용하여 단어들을 구분. 명사로만 구성.|`module.py`,`my_module.py`|
|패키지 (package)|소문자만 사용. 다만 `_`를 사용하여 단어들을 구분하지 않음.* 명사로만 구성|`package`,`mypackage`|
#### 지양할 것 (xx)
- 특별한 의미가 없거나 목적이 불분명한 이름
- 너무 자세하거나 긴 이름들
- 너무 짧은 이름들
- 단어 철자를 짧게 만든 이름들
## Space
- 빈 줄은 한 줄. 또한 빈줄은 관련이 있는 로직(login) 단위로 삽입한다.  
- 일반적으로 한 줄에는 79자를 안넘어가도록 코드를 작성하지만, 한 눈에 봤을때 부담스럽다면 다음줄로 나누어서 작성하여 가독성을 높일 것.  
  (같은 함수 내 로직이 여러 부분일 때 사이에 빈 줄 삽입)
## Code Align
컨벤션 정렬을 잘 하자.
```python
import json, bcrypt, jwt

from django.views           import View
from django.http            import JsonResponse, HttpResponse
from django.core.exceptions import ValidationError

from .models                import User
from my_settings            import SECRET_KEY, DATABASES, ALGORITHM
```
