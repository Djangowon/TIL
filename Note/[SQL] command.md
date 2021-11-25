# MySql command
#### SQL (Structured Query Language)
- 데이터베이스 시스템에서 자료를 처리하는 용도로 사용되는 구조적 데이터 질의 언어
#### MySQL
- 오픈 소스의 관계형 데이터베이스 관리 시스템(RDBMS)
#### CRUD (Create, Read, Update, Delete)
- 기본적으로 데이터를 생성, 읽기, 갱신, 삭제하는 것
---
#### Create
- 테이블 생성
```
create table student (
칼럼명 타입 조건(not null 등),
칼럼명 타입 조건(not null 등),
칼럼명 타입 조건(not null 등),
PRIMARY KEY ~~ );
```
#### Insert
- 테이블에 데이터 삽입
```
insert into student values(테이블에 맞는 데이터 양식);
```
#### Update
- 데이터 내용 수정
```
update 테이블 set 칼럼 = '값' where 조건;
```
#### Delete
- 데이터 삭제
```
delete from 테이블 where 조건;
```
#### select
- 모든 컬럼 조회
```
select * from student;
```
- 필요한 컬럼 조회
```
select age, name from student;
```

## DML(Data Manipulation Language) : 데이터 조작어
- 테이블에 데이터를 검색, 삽입, 수정, 삭제하는 데 사용하며 SELECT, INSERT, DELETE, UPDATE 문 등이 있다. 여기서 SELECT 문은 특별히 질의어(query)라고 부른다.

## DDL(Data Definition Language) : 데이터 정의어
- 테이블이나 관계의 구조를 생성하는 데 사용하며 CREATE, ALTER, DROP 등이 있다.
- 
## DCL(Data Control Language) : 데이터 제어어 
- 데이터의 사용 권한을 관리하는 데 사용하며 GRANT, REVOKE 문 등이 있다.

## TCL(Transaction Control Language) : 트랜젝션 제어
- COMMIT, ROLLBACK, SAVEPOINT 등이 있다.


