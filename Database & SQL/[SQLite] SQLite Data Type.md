# SQLite Date Type

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
