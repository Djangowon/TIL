# About JPA, JPQL


<br>
<br>

## 데이터베이스 방언
* JPA는 특정 데이터베이스에 종속적이지 않도록 설계되어 있음
* 각각의 데이터베이스가 제공하는 SQL 문법과 함수는 조금씩 다름
	* 가변 문자: MySQL은 VARCHAR, Oracle은 VARCHAR2
	* 문자열을 자르는 함수: SQL 표준은 SUBSTRING(), Oracle은 SUBSTR()
	* 페이징: MySQL은 LIMIT, Oracle은 ROWNUM
* 방언: SQL 표준을 지키지 않는 특정 데이터베이스만의 고유한 기능

<br>
<br>


## JPA 설정하기
/resources/META-INF/persistence.xml
```java
<persistence-unit name="hello">
        <properties>
            <!-- 필수 속성 -->
            <property name="javax.persistence.jdbc.driver" value="org.h2.Driver"/>
            <property name="javax.persistence.jdbc.user" value="sa"/>
            <property name="javax.persistence.jdbc.password" value=""/>
            <property name="javax.persistence.jdbc.url" value="jdbc:h2:tcp://localhost/~/test"/>
            <property name="hibernate.dialect" value="org.hibernate.dialect.H2Dialect"/> //value="org.hibernate.dialect.MySQLDialect" 
            <!-- 옵션 -->
            <property name="hibernate.show_sql" value="true"/>
            <property name="hibernate.format_sql" value="true"/>
            <property name="hibernate.use_sql_comments" value="true"/>
            <!--<property name="hibernate.hbm2ddl.auto" value="create" />-->
        </properties>
    </persistence-unit>
```
* javax 라는 것은 표준을 지키는 것
* hibernate.dialect는 JPA 방언이라고 부름
* 각 DB의 조금씩 다른 문법을 JPA는 dialect를 통해 맞춰줌


<br>
<br>

## JPA 사용하기
* jpa에서는 트랜잭션 단위가 중요함
* 모든 데이터를 변경하는 모든 작업은 트랜잭션 안에서 작업을 해주어야 함


<br>
<br>


```java
<property name="hibernate.show_sql" value="true"/> //쿼리를 보여주는 옵션  
<property name="hibernate.format_sql" value="true"/> //쿼리를 보기 좋게 포매팅 시켜주는 옵션  
<property name="hibernate.use_sql_comments" value="true"/> //쿼리가 왜 나왔는지 알려주는 옵션 (쿼리문 앞에 붙는 주석부분)
```

```
Hibernate: 
    /* insert hellojpa.Member
        */ insert 
        into
            Member
            (name, id) 
        values
            (?, ?)
```

<br>
<br>

* 수정하고 저장(persist())을 안 해도 되는 이유? 
  * jpa를 통해서 엔티티를 가져오면 jpa가 관리를 하는데, jpa는 변경 유무를 트랜잭션을 커밋하는 시점에 다 체크를 함


<br>
<br>


## 주의
* 엔티티 매니저 팩토리는 하나만 생성해서 애플리케이션 전체에서 공유함
* 엔티티 매니저는 쓰레드간에 공유하면 안됨(사용하고 버려야 함)
* JPA의 모든 데이터 변경은 트랜잭션 안에서 실행해야 함


<br>
<br>

# JPQL
> JPQL을 한마디로 정의하면 객체 지향 SQL
* 가장 단순한 조회 방법
	* EntityManager.find()  
	* 객체 그래프 탐색(a.getB().getC())

<br>

* JPA는 SQL을 추상화한 JPQL이라는 객체 지향 쿼리 언어 제공
* SQL과 유사한 문법
	* SELECT, FROM, WHERE, GROUP BY, HAVING, JOIN 지원
* JPQL은 엔티티 객체를 대상으로 쿼리
* SQL은 데이터베이스 테이블을 대상으로 쿼리

<br>

* JPQL 장점: 데이터베이스(방언)를 바꾸어도 JPQL 자체 코드를 바꾸지 않아도 됨
* SQL을 추상화해서 특정 데이터베이스 SQL에 의존적이지 않음

<br>

* [JPQL은 객체를 대상으로 하는 객체지향 쿼리](#JPQL)
	* JPA를 사용하면 엔티티 객체를 중심으로 개발하게 되는데, 문제는 검색 쿼리임
	* 검색을 할 때도 테이블이 아닌 엔티티 객체를 대상으로 검색
	* 모든 DB 데이터를 객체로 변환해서 검색하는 것은 불가능함
	* 애플리케이션이 필요한 데이터만 DB에서 불러오려면 결국 검색 조건이 포함된 SQL이 필요함
