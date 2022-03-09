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
