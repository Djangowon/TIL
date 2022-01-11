# SQLite Data Type
SQLite에는 다음 네 가지 기본 데이터 형식만 있습니다. INTEGER, REAL, TEXT 및 BLOB. 데이터베이스 값을 object로 반환하는 API는 이 네 가지 형식 중 하나만 반환합니다. 추가 .NET 형식은 Microsoft.Data.Sqlite에서 지원되지만 값은 궁극적으로 다음 형식과 네 가지 기본 형식 중 하나 사이에서 강제 변환됩니다.

|.NET|SQLite|설명|
|:---|:---|:---|
|Boolean|INTEGER|0 또는 1|
|Byte|INTEGER|
|Byte[]|BLOB|	
|Char|TEXT|UTF-8|
|DateTime|TEXT|yyyy-MM-dd HH:mm:ss.FFFFFFF|
|DateTimeOffset|TEXT|yyyy-MM-dd HH:mm:ss.FFFFFFFzzz|
|Decimal|TEXT|0.0########################### 형식. REAL은 손실 형식입니다.|
|Double|real||
|GUID|TEXT|00000000-0000-0000-0000-000000000000|
|Int16|INTEGER||	
|Int32|INTEGER||
|Int64|INTEGER||
|SByte|INTEGER||	
|Single|real||
|String|TEXT|UTF-8|
|TimeSpan|TEXT|d.hh:mm:ss.fffffff|
|UInt16|INTEGER||	
|UInt32|INTEGER||
|UInt64|INTEGER|큰 값 오버플로|

[참고](https://www.sqlite.org/datatype3.html/)  
[참고](https://docs.microsoft.com/ko-kr/dotnet/standard/data/sqlite/types/)
