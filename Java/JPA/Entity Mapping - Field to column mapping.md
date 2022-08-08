# Entity Mapping - Field to column mapping

<br>
<br>

## 필드와 컬럼 매핑
### 매핑 어노테이션

|어노테이션|설명|
|:---|:---|
|@Column|컬럼 매핑|
|@Temporal|날짜 타입 매핑|
|@Enumerated|enum 타입 매핑|
|@Lob|BLOB, CLOB 매핑|
|@Transient|특정 필드를 컬럼에 매핑하지 않음(매핑 무시)|


<br>
<br>


## @Column
|속성|설명|기본값|
|:---:|:---|:---|
|name|필드와 매핑할 테이블의 컬럼 이름|객체의 필드 이름|
|insertable, updatable|등록, 변경 가능 여부|TRUE|
|nullable(DDL)|null 값의 허용 여부를 설정함. false로 설정하면 DDL생성 시에 not null 제약조건이 붙음||
|unique(DDL)|@Table의 uniqueConstraints와 같지만 한 컬럼에 간단히 유니크 제약조건을 걸 때 사용함||
|length(DDL)|문자 길이 제약조건, String 타입에만 사용함|255|
|precision, scale(DDL)|BigDecimal 타입에서 사용함(BigInteger도 사용가능) </br> precision은 소수점을 포함한 전체 자릿수를, scale은 소수의 자릿수임 </br> 참고로 double, float타입에는 적용되지 않음 </br> 아주 큰 숫자나 정밀한 소수를 다루어야 할 때만 사용함|percision=19, scale=2|


<br>
<br>


## @Enumerated
* 자바 enum 타입을 매핑할 때 사용함
* 주의할 점: *ORDINAL 사용 X* 
	* 운영 상에서 EnumType에 ORDINAL 쓰면 굉장히 위험함 -> EnumType.String 으로 사용할 것

|속성|설명|기본값|
|:---:|:---|:---|
|value|- EnumType.ORDINAL: enum 순서를 데이터베이스에 저장</br> - EnumType.STRING: enum 이름을 데이터베이스에 저장|EnumType.ORDINAL|


<br>
<br>

## @Temporal
* 날짜 타입(java.util.Date, java.util.Calendar)을 매핑할 때 사용함
* 참고: LocalDate, LocalDateTime을 사용할 때는 생략 가능함(최신 하이버네이트 지원)

|속성|설명|기본값|
|:---:|:---|:---|
|value|- TemporalType.DATE: 날짜, 데이터베이스 date 타입과 매핑 </br> - TemporalType.TIME: 시간, 데이터베이스 time 타입과 매핑 </br> - TemporalType.TIMESTAMP: 날짜와 시간, 데이터베이스 timestamp 타입과 매핑||


<br>
<br>

## @Lob
* 데이터베이스 BLOB, CLOB 타입과 매핑
	* @Lob에는 지정할 수 있는 속성이 없음
	* 매핑하는 필드 타입이 문자면 CLOB 매핑, 나머지는 BLOB 매핑
		* CLOB: String, char[], java.sql.CLOB
		* BLOB: byte[], java.sql.BLOB


<br>
<br>

## Ref
https://www.inflearn.com/course/ORM-JPA-Basic
