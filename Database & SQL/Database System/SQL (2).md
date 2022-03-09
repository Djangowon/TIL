# SQL
## 데이터 조작 언어의 개념
### DML: Data Manipulation Language
* 정의된 테이블에 레코드를 삽입・수정・삭제 및 검색하는데 사용되는 명령어의 집합
* 명령어의 종류
    * INSERT - 테이블 스키마에 적합한 레코드를 삽입
    * UPDATE - 테이블에서 조건을 만족하는 특정 레코드의 컬럼값을 수정
    * DELETE - 테이블에 조건을 만족하는 특정 레코드를 삭제
    * SELECT - 조건을 만족하는 레코드를 테이블에서 검색

### INSERT
* 테이블에 새로운 레코드를 삽입하는 명령문
    * 테이블에 새로운 레코드를 삽입
    * 모든 속성 또는 부분 속성에 대한 속성값을 삽입
> INSERT INTO 테이블이름 VALUES(값₁,값₂,・・・값𝗇)  
> INSERT INTO 테이블이름(컬럼₁,컬럼₂, ・・・컬럼𝗆) VALUES(값₁,값₂,・・・값𝗆)

### UPDATE
* 조건을 만족하는 레코드의 특정 컬럼값을 수정
> UPDATE 테이블이름 SET 컬럼₁=값₁[,컬럼₂=값₂,・・・, 컬럼𝗇=값𝗇] [WHERE 조건]  
> UPDATE 테이블이름 SET 컬럼₁=수식₁[,컬럼₂=수식₂,・・・, 컬럼𝗇=수식𝗇] [WHERE 조건]

### DELETE
* 조건에 일치하는 레코드 집합을 테이블에서 삭제할 때 사용하는 명령어    
> DELETE FROM 테이블이름 [WHERE 조건]

### SAFE UPDATES 모드
* WHERE절이 없는 UPDATE/DELETE 문은 테이블의 전체 레코드를 변경/삭제
* 의도하지 않은 데이터 변경/삭제 방지를 위해 MySQL은 SAFE UPDATES 모드를 지원
* 기본키가 아닌 컬럼을 대상으로 수정/삭제 조건을 명시할 경우 실행 여부를 결정
> SET SQL_SAFE_UPDATES = 0 또는 1

### SELECT
* 한 개 이상의 테이블에서 주어진 조건에 만족하는 레코드를 출력하는 명령문
* 관계 대수의 셀렉션, 프로젝션, 조인, 카티션 프로덕트 연산자의 기능을 모두 포함하는 명령문
* 필수적 절인 SELECT 절과 부가적인 목적으로 사용할 수 있는 여러 절을 혼합하여 검색 기능을 구체화
> SELECT [DISTICT] 컬럼₁,컬럼₂,・・・,컬럼𝗇  
> FROM 테이블₁[INNER JOIN|OUTER JOIN  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;테이블₂, INNER JOIN|OUTER JOIN  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ON 조인 조건₁  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;테이블₃  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;・・・, INNER JOIN|OUTER JOIN  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;테이블𝗆]  
> [ON 조인 조건식]  
> [WHERE 조건식[중첩질의]]  
> [GROUP BY 컬럼₁,컬럼₂,・・・,컬럼𝗒  
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[HAVING 조건]]  
> [ORDER BY 컬럼₁[ASC|DESC], ・・・,컬럼𝗓[ASC|DESC]]

### SELECT 문의 각 절의 기능
* SELECT절 - 결과에 포함되는 컬럼을 지정
* FROM절 - 질의를 적용할 테이블을 지정
* ON/WHERE절 - 조인 조건/검색할 레코드 조건을 지정
* GROUP BY절 - 레코드를 그룹화하기 위한 그룹 조건을 지정
* HAVING절 - GROUP BY절이 적용된 결과에 조건을 지정
* ORDER BY절 - 검색 결과의 정렬 기준을 지정

### 단순질의문
* 레코드를 제한하지 않고 전체 테이블을 검색하는 SELECT 문으로 WHERE절이 없는 질의문
> SELECT 컬럼₁,컬럼₂,・・・,컬럼𝗇 FROM 테이블  
> SELECT * FROM 테이블

#### SELECT DISTINT = 중복제거할 때 사용

### 조건질의문
* 산술연삭식, 함수 등을 사용하여 표현한 조건을 WHERE절에 기술하여 조건을 만족하는 레코드만 검색하는 SELECT문
    * 산술연산자
        * SELECT절 또는 WHERE절에 사용되어 컬럼값 또는 상수와의 산술 계산을 위한 연산자
    * 비교연산자
        * 컬럼값과 상수 또는 컬럼값과 다른 컬럼값과의 크기를 비교하는 연산자
    * 논리연산자
        * 두 개 이상의 조건이 기술되는 질의문에서 조건식 간의 관계를 정의하는 연산자

* WHERE절은 UPDATE, DELETE문에서도 동일하게 적용

### 데이터 정렬
* ORDER BY절을 사용
* 검색 결과를 특정 컬럼에 대해 오름차순 또는 내림차순으로 정렬
    * 오름차순: ASC
    * 내림차순: DESC
> SELECT문 형식 ORDER BY 컬럼₁,[ASC|DESC],・・・,컬럼𝗇[ASC|DESC]

### 특수연산자
* 범위 포함 여부, 부분 일치 여부, 포함 여부 등 관계형 데이터베이스에서만 사용되도록 고안된 연산자
    * BETWEEN 
    * LIKE 부분일치검색
    * IN

### 함수의 개념
* 특정 목적을 수행하도록 사전에 정의된 연산 및 기능을 수행한 후 결과값을 반환하는 명령어 집합
* 상용 DBMS는 검색결과가 사용자에게 여러 형태로 사용되도록 여러 데이터 타입에 대한 다양한 함수를 제공(MySQL 기준)
    * 문자함수
        * 문자열 조작 및 문자 형식 변환 등의 문자와 관련된 다양한 연산을 지원하는 함수
    * 숫자함수
        * 삼각함수, 상수, 올림과 버림, 난수 등의 숫자 데이터 타입에 적용할 수 있는 계산을 위한 함수
    * 날짜 및 시간함수
        * 날짜 및 시간 데이터 타입에 적용되어 산술 연산 및 시간 형 변환 등의 조작을 위한 함수

