## Problems with SQL-centric development

<br>
<br> 


## 객체와 관계형 데이터베이스의 차이

> 관계형 데이터 베이스는 데이터를 잘 정규화해서 보관하는 것이 목표  
> 객체는 필드나 메서드 등 묶여서 캡슐화해서 사용하는 것이 목표


* 상속
	* 자바 컬렉션에서 조회하는 것은 단순함
	* 관계형 데이터베이스를 사용하는 순간 join과 Mapping 작업을 일일이 해줘야하기 때문에 번잡함
* 연관관계
	* 객체는 참조를 사용함
		* member.getTeam()
		* 한방향
		 객체 모델링, 자바 컬렉션에 관리하면 쉬움
		* 객체 그래프 탐색: 객체는 자유롭게 객체 그래프를 탐색할 수 있어야 함
	* 테이블은 외래 키를 사용함
		* JOIN ON M.TEAM_ID = T.TEAM_ID
		* 양방향
		* SQL을 직접 다루게 되면 계층형 아키텍처에서 진정한 의미의 계층 분할이 어려움
		* 객체답게 모델링을 할 수록 매핑 작업만 늘어남
			> 결국, 객체를 자바 컬렉션에 저장하듯이 DB에 저장하기위해 JPA를 사용함
* 데이터 타입
* 데이터 식별 방법


<br>
<br> 


# JPA

* Java Persistence API
* 자바 진영의 ORM 기술 표준

## ORM
* Object-relational mapping(객체 관계 매핑)
* 객체는 객체대로 설계
* 관계형 데이터베이스는 관계형 데이터베이스대로 설계
* ORM 프레임워크가 중간에서 매핑
* 대중적인 언어에는 대부분 ORM 기술이 존재함


<br>
<br> 


> JPA는 애플리케이션과 JDBC 사이에서 동작함  
> JPA가 JDBC API를 사용해서 적절한 쿼리를 만들고 결과 값을 받아서 객체에 매핑(ResultSet 매핑)을 해주고, 패러다임 불일치를 해결함


## JPA는 표준 명세
* JPA는 인터페이스의 모음임
* JPA 2.1 표준 명세를 구현한 3가지 구현체
* 하이버네이트(대표적), EclipseLink, DataNucleus

## JPA를 사용해야 하는 이유
* SQL 중심적인 개발에서 객체 중심으로 개발할 수 있음
* [생산성](#생산성---JPA와-CRUD)
* [유지보수](#유지보수)
    * 유지보수 - JPA: 필드만 추가하면 됨, SQL은 JPA가 처리

* [패러다임의 불일치 해결](#JPA와-패러다임의-불일치-해결)
* [성능](#JPA의-성능-최적화-기능)
* 데이터 접근 추상화와 벤더 독립성
* 표준


<br>
<br> 



## 생산성 - JPA와 CRUD
* 저장: jpa.persist(member)
* 조회: Member member = jpa.find(memberId)
* 수정: member.setName("변경할 이름")
* 삭제: jpa.remove(member)



<br>
<br> 


## JPA와 패러다임의 불일치 해결
* JPA와 상속 - 저장
	* 객체가 상속관계라고 해도 데이터 베이스에 집어넣을 땐 두개의 테이블에 나눠서 넣어줘야 함
	* 즉, 쿼리가 두개 짜여져야 하는데 이런 부분을 JPA가 알아서 두개의 쿼리를 만들어줌
* JPA와 상속 - 조회
	* 가져오고 싶은 상속관계인 데이터 타입의 식별자를 넘기면 JPA가 알아서 JOIN해서 가져옴
* JPA와 연관관계, 객체 그래프 탐색
	* 신뢰할 수 있는 엔티티, 계층
	* JPA를 통해서 객체를 가져오려면 객체 그래프를 자유롭게 탐색할 수 있음
	* JPA의 지연로딩 기능
		* 실제 객체를 조회해서 사용하는 시점에 SQL 쿼리가 나가서 데이터가 채워지는 기능임
* JPA와 비교하기
	* 동일한 트랜잭션에서 조회한 엔티티는 같음을 보장



<br>
<br> 



## JPA의 성능 최적화 기능
* [1차 캐시와 동일성(identity)보장](#1차-캐시와-동일성(identity)보장)
* [트랜잭션을 지원하는 쓰기 지연(transactional write-behind)](트랜잭션을-지원하는-쓰기-지연---INSERT)
* [지연 로딩(Lazy Loading)](지연-로딩과-즉시-로딩)


<br>
<br> 


## 1차 캐시와 동일성(identity)보장
* 같은 트랜잭션 안에서는 같은 엔티티를 반환 - 약간의 조회 성능 향상
```java
String memberId = "99";
Member m1 = jpa.find(Member.class, memberId); //SQL
Member m2 = jpa.find(Member.class, memberId); //캐시

println(m1 == m2) //true
```
* DB Isolation Level이 Read Commit이어도 애플리케이션에서 Repeatable Read 보장



<br>
<br> 



## 트랜잭션을 지원하는 쓰기 지연 - INSERT
* 트랜잭션을 커밋할 때까지 INSERT SQL을 모음
* JDBC BATCH SQL 기능을 사용해서 한번에 SQL 전송
```java
transaction.begin(); //[트랜잭션] 시작

em.persist(memberA);
em.persist(memberB);
em.persist(memberC);
//여기까지 INSERT SQL을 데이터베이스에 보내지 않음

//커밋하는 순간 데이터베이스에 INSERT SQL을 모아서 보냄
transaction.commit(); //[트랜잭션] 커밋
```



<br>
<br> 



## 트랜잭션을 지원하는 쓰기 지연 - UPDATE
* UPDATE, DELETE로 인한 로우(ROW)락 시간 최소화
* 트랜잭션 커밋 시 UPDATE, DELETE SQL 실행하고, 바로 커밋



<br>
<br> 



## 지연 로딩과 즉시 로딩
* 지연 로딩: 객체가 실제 사용될 때 로딩
* 즉시 로딩: JOIN SQL로 한번에 연관된 객체까지 미리 조회
* JPA에서 옵션 하나로 지연 로딩와 즉시 로딩을 스위치 껐다 켰다 하듯이 가능함




<br>
<br> 

## Ref
https://www.inflearn.com/course/ORM-JPA-Basic
