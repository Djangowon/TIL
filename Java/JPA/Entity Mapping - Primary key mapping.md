# Entity Mapping - Primary key mapping


<br>
<br>


## 기본 키 매핑 어노테이션
* @Id
* @GeneratedValue



## 기본 키 매핑 방법
* 직접 할당: @Id만 사용
* 자동 생성(@GeneratedValue)
	* IDENTITY: 데이터베이스에 위임, MySQL
	* SEQUENCE: 데이터베이스 시퀀스 오브젝트 사용, ORACLE
		* @SequenceGenerator 필요
	* TABLE: 키 생성용 테이블 사용, 모든 DB에서 사용
		* @TableGenerator 필요
	* AUTO: 방언에 따라 자동 지정, 기본값


<br>
<br>


## IDENTITY 전략 - 특징

* 기본 키 생성을 데이터베이스에 위임  
* 주로 MySQL, PostgreSQL, SQL Server, DB2에서 사용
	* (예: MySQL의 AUTO_ INCREMENT)
* JPA는 보통 트랜잭션 커밋 시점에 INSERT SQL 실행
* AUTO_ INCREMENT는 데이터베이스에 INSERT SQL을 실행한 이후에 ID 값을 알 수 있음
* IDENTITY 전략은 em.persist() 시점에 즉시 INSERT SQL 실행 하고 DB에서 식별자를 조회함
	> IDENTITY 전략은 데이터베이스에 값이 들어가야 PK인 ID값을 알 수 있기 때문에.
	
```java
public class Member {

	@Id
	@GeneratedValue(strategy = GenerationType.IDENTITY)
	private Long id;
```


<br>
<br>


## SEQUENCE 전략 - 특징

* 데이터베이스 시퀀스는 유일한 값을 순서대로 생성하는 특별한 오브젝트임(ex. 오라클 시퀀스)
* 오라클, PostgreSQL, DB2, H2 데이터베이스에서 사용함

```java
@Entity
@SequenceGenerator(
		name = “MEMBER_SEQ_GENERATOR",
		sequenceName = “MEMBER_SEQ", //매핑할 데이터베이스 시퀀스 이름
		initialValue = 1, allocationSize = 1)
public class Member {

	@Id
	@GeneratedValue(strategy = GenerationType.SEQUENCE,
			generator = "MEMBER_SEQ_GENERATOR")
	private Long id;
```


<br>

## SEQUENCE - @SequenceGenerator
* 주의: allocationSize 기본값은 50임

|속성|설명|기본값|
|:---|:---|:---|
|name|식별자 생성기 이름|필수|
|sequenceName|데이터베이스에 등록되어 있는 시퀀스 이름|hibernate_sequence|
|initialValue|DDL 생성 시에만 사용됨, 시퀀스 DDL을 생성할 때 처음 1 시작하는 수를 지정함|1|
|allocationSize|시퀀스 한 번 호출에 증가하는 수(성능 최적화에 사용됨) </br>데이터베이스 시퀀스 값이 하나씩 증가하도록 설정되어 있으면 이 값을 반드시 1로 설정해야 함|50|
|catalog, schema|데이터베이스 catalog, schema 이름||



<br>
<br>


## TABLE 전략 
* 생성 전용 테이블을 하나 만들어서 데이터베이스 시퀀스를 흉내내는 전략
* 장점: 모든 데이터베이스에 적용 가능 
* 단점: 성능

```java
@Entity
@TableGenerator(
		name = "MEMBER_SEQ_GENERATOR",
		table = "MY_SEQUENCES",
		pkColumnValue = “MEMBER_SEQ", allocationSize = 1)
public class Member {

	@Id
	@GeneratedValue(strategy = GenerationType.TABLE,
			generator = "MEMBER_SEQ_GENERATOR")
	private Long id;
```

<br>

|속성|설명|기본값|
|:---|:---|:---|
|name|식별자 생성기 이름|필수|
|table|키생성 테이블명|hibernate_sequences|
|pkColumnName|시퀀스 컬럼명|sequence_name|
|valueColumnName|시퀀스 값 컬럼명|next_val|
|initialValue|초기 값, 마지막으로 생성된 값이 기준임|0|
|allocationSize|시퀀스 한 번 호출에 증가하는 수(성능 최적화에 사용됨)|50|
|catalog, schema|데이터베이스 catalog, schema 이름||
|uniqueConstraints(DDL)|유니크 제약 조건을 지정할 수 있음||


<br>
<br>


## 권장하는 식별자 전략
* 기본 키 제약 조건은 null이 아니어야 하고, 유일해야 하고, 변하면 안됨
* 미래까지 이 조건을 만족하는 자연키는 찾기 어려움, 대리키(대체키)를 사용함
* 권장하는 방법: Type은 Long형 + 대체 키(Auto Increment나 시퀀스나 uuid) + 키 생성 전략 사용하는 법


<br>
<br>

## Ref
https://www.inflearn.com/course/ORM-JPA-Basic
