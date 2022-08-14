# mock이란?

쉽게 말해 ‘가짜’ 데이터라고 이해하면 된다.

예를 들어 테스트 코드를 작성할 때, 실제 모듈과 유사하게 동작하는 가짜 데이터를 만들어 사용할 수 있다.

<br>

### ‘가짜’ 데이터인 ‘mock’을 왜 사용하는 걸까?

테스트하려는 함수가 10초 이상의 연산 시간이 필요한 모듈에 의존하고 있다고 가정해보자. 우리는 해당 함수를 테스트할 때마다 매번 10초를 기다려야 한다. 이는 개발 생산성을 크게 저하시킬 것이다.

의존하고 있는 모듈로 인해 본 코드를 테스트하기 어려울 때, mock을 사용하면 해당 모듈을 실행하지 않고도 해당 테스트를 검증할 수 있다. 우리는 모듈의 응답을 mock으로 대체함으로써 본 코드의 테스트에 집중할 수 있다. 

이처럼 성능 저하, 비용 등 불필요한 리소스 발생이 예상될 때, 일반적으로 mock 사용을 권장한다.

이번 글에서는 unittest mock과 pytest mock 두 가지 mock 사용법에 대해 설명하겠다.

<br><br>


# unittest mock 사용법

먼저 mock으로 대체할 ‘target\_mock’이라는 함수를 만들어보자.

```py
# tests/file.py

def target_mock():
    return "mock 실패!"
```

테스트를 하기 위한 ‘test\_mock.py’ 파일을 생성하자. 아래 코드는 전체 코드이다.

```py
# tests/test_mock.py

from unittest import mock
from tests import file

@mock.patch("tests.file.target_mock", return_value="mock 성공!")
def test_mock(self):
    actual = file.target_mock()
    expected = "mock 성공!"

    assert actual is expected
```

먼저 unittest 의 mock을 Import 한다.

```py
from unittest import mock
```

mock을 사용하기 위해 테스트 함수 위에 데코레이터를 추가한다.

```py
@mock.patch("tests.file.target_mock", return_value="mock 성공!")
```

patch 매서드의 첫 번째 인자는 타깃 함수의 경로이다.

return\_value 인자에는 타깃 함수의 반환 값을 지정할 수 있다.

테스트 함수는 다음과 같다.

```py
def test_mock(self):
    actual = file.target_mock()
    expected = "mock 성공!"

    assert actual is expected
```

unittest mock을 사용하기 위해서는 함수 인자로 self를 넣어주어야 한다.

actual 은 타겟 함수를 호출한 값, expected 은 우리가 예상한 값이다. (우리가 지정한 mock 반환 값)

이제 테스트를 실행해보면 테스트가 성공하는 것을 볼 수 있다.


<br><br>


# pytest mock 사용법

이번에는 pytest-mock 라이브러리를 사용한 mock 사용법이다.

이번에도 ‘target\_mock’이라는 함수를 mocking 해보겠다.

```py
# tests/file.py

def target_mock():
    return "mock 실패!"
```

pytest-mock 라이브러리를 설치한다.

```
pip install pytest-mock
```

아래 코드는 전체 코드이다.

```py
# tests/test_mock.py

from tests import file

def test_mock(mocker):
    mocker.patch("tests.file.target_mock", return_value="mock 성공!")

    actual = file.target_mock()
    expected = "mock 성공!"

    assert actual is expected
```

pytest-mock을 설치하면 mock을 따로 import 하지 않고도 ‘mocker’라는 인자는 테스트 함수에 넣을 수 있다. 이는 fixture로 작동하기 때문인데 mocker 인자가 어디서 오는지 헷갈리지 않도록 조심하자!

\*fixture에 대해 궁금하다면 해당 글을 참고하자.

[2022.04.14 - \[Dev/Debug\] - @pytest.fixture 로 test 데이터 세팅하기](https://daco2020.tistory.com/305)

테스트 함수의 달라진 점을 살펴보자

```py
def test_mock(mocker):
    mocker.patch("tests.file.target_mock", return_value="mock 성공!")

    actual = file.target_mock()
    expected = "mock 성공!"

    assert actual is expected
```

unittest mock을 사용할 때에는 mock 데코레이터를 사용했는데 이번에는 mocker라는 인자를 통해 함수 내부로 이동했다. 그 외에는 동일하게 구현되어있다. 

테스트를 실행해보면 마찬가지로 성공하는 것을 볼 수 있다.

[##_Image|kage@Tmn3L/btrJB4salw3/sgoB36S2Jl23qYDfp323OK/img.png|CDM|1.3|{"originWidth":1280,"originHeight":82,"style":"alignCenter"}_##]

pytest-mock는 데코레이터가 아닌 fixture 기반이므로 mock을 더 직관적으로 사용할 수 있다는 장점이 있다.

<br><br>

# mock 주의할 점

mock 사용법에 대해 간단히 알아보았다. mock은 분명 테스트를 더 쉽게 만들어 준다.

하지만 mock을 남발해서는 안된다. 만약 mock으로 생성한 데이터가 잘못된 데이터라면? 테스트는 잘못된 데이터임을 인지하지 못하고 계속해서 성공을 내보낼 수 있다.

때문에 어떤 모듈을 리팩터링한다면 해당 모듈을 Mocking 하고 있는 다른 테스트들도 점검해야 한다. 그래야 mock을 우리의 의도대로 유지할 수 있다.

<br><br>


### 레퍼런스

[pytest-mock](https://pypi.org/project/pytest-mock/) <br>
[unittest.mock](https://docs.python.org/3/library/unittest.mock.html)