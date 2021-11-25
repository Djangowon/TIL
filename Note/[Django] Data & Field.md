# Data
데이터베이스 테이블의 각 열에는 이름과 데이터 유형이 있어야 한다.
SQL 개발자는 테이블을 생성할 때 각 열에 저장할 데이터 유형을 결정해야 하고, 데이터 유형은 SQL이 각 열 내부에 예상되는 데이터 유형을 이해하기 위한 지침이며 SQL이 저장된 데이터와 상호 작용하는 방식을 식별한다.

## 자주 쓰이는 Field types 
|Field type|설명|
|:---:|:---:|
|CharField|제한된 문자열 필드 타입. 최대 길이를 max_length 옵션에 지정해야 한다. 문자열의 특별한 용도에 따라 CharField의 파생클래스로서, 이메일 주소를 체크를 하는 EmailField, IP 주소를 체크를 하는 GenericIPAddressField, 콤마로 정수를 분리한 CommaSeparatedIntegerField, 특정 폴더의 파일 패스를 표현하는 FilePathField, URL을 표현하는 URLField 등이 있다.|
|TextField|대용량 문자열을 갖는 필드|
|IntegerField|32 비트 정수형 필드. 정수 사이즈에 따라 BigIntegerField, SmallIntegerField 을 사용할 수도 있다.|
|BooleanField|true/false 필드. Null 을 허용하기 위해서는 NullBooleanField를 사용한다.|
|DateTimeField|날짜와 시간을 갖는 필드. 날짜만 가질 경우는 DateField, 시간만 가질 경우는 TimeField를 사용한다.|
|DecimalField|소숫점을 갖는 decimal 필드|
|BinaryField|바이너리 데이타를 저장하는 필드|
|FileField|파일 업로드 필드|
|ImageField|FileField의 파생클래스로서 이미지 파일인지 체크한다.|
|UUIDField|GUID (UUID)를 저장하는 필드|
|TextField|대용량 문자열을 갖는 필드|

## 자주 쓰이는 Field Options 
모델의 필드는 필드 타입에 따라 여러 옵션(혹은 Argument)를 가질 수 있다. 예를 들어, CharField는 문자열 최대 길이를 의미하는 max_length 라는 옵션을 갖는다. 필드 옵션은 일반적으로 생성자에서 아규먼트로 지정한다. 다음은 모든 필드 타입에 적용 가능한 옵션들 중 자주 사용되는 몇가지를 요약한 것이다.
|Field Option|설명|
|:---:|:---:|
|null (Field.null)|null=True 이면, Empty 값을 DB에 NULL로 저장한다. DB에서 Null이 허용된다. 예: models.IntegerField(null=True)|
|blank (Field.blank)|blank=False 이면, 필드가 Required 필드이다. blank=True 이면, Optional 필드이다. 예: models.DateTimeField(blank=True)|
|primary_key (Field.primary_key)|해당 필드가 Primary Key임을 표시한다. 예: models.CharField(max_length=10, primary_key=True)|
|unique (Field.unique)|해당 필드가 테이블에서 Unique함을 표시한다. 해당 컬럼에 대해 Unique Index를 생성한다. 예: models.IntegerField(unique=True)|
|default (Field.default)|필드의 디폴트값을 지정한다. 예: models.CharField(max_length=2, default="WA")|
|db_column (Field.db_column)|컬럼명은 디폴트로 필드명을 사용하는데, 만약 다르게 쓸 경우 지정한다.|

이 외에는 공식문서로 확인하자.  
[공식문서](https://docs.djangoproject.com/en/1.11/ref/models/fields/#field-types/)  
[공식문서](https://www.w3schools.com/sql/sql_datatypes.asp/)  
