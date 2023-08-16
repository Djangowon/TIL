# JPA 
> Java Persistence API  
> 자바 진영의 ORM 기술 표준

## ORM
Object relational mapping (객체 관계 매핑)
객체와 관계형 데이터베이스랑 매핑을 시켜주는 것.
객체는 객체대로 설계하고 관계형 db는 관계형 db대로 설계
ORM 프레임워크가 중간에서 매핑 -> 패러다임의 불일치를 해결해주는 것.
대부분의 대중적인 언어에는 ORM이 존재함

<br>

- JPA는 애플리케이션과 JDBC 사이에서 동작한다.

<br>

> EJB(자바 표준) -> 하이버네이트(오픈 소스) -> JPA(자바 표준)  
> 즉, 오픈소스에서 출발한 표준임  
> 실용적인데서 온 자바 표준이기 때문에 오랫동안 사랑받은 것 같음  

<br>
<br>

## JPA를 왜 사용해야 하는가?
- SQL 중심적인 개발에서 객체 중심으로 개발할 수 있음
	- 자바 컬렉션에 객체를 저장하듯이 조회하듯이 던지기만 하면 됨
- 생산성, 유지보수 용이
- 패러다임의 불일치 해결
- 성능
- [데이터 접근 추상화와 벤더 독립성](https://dololak.tistory.com/465)
- 표준


<br>
<br>


## 생산성 - JPA와 CRUD
* 저장 : jpa.persist(member)
* 조회 : Member member = jpa.find(memberId)
* 수정 : member.setName("변경할 이름")
* 삭제 : jpa.remove(member)

<br>
<br>


## 유지보수 
- 기존: 필드 변경시 모든 SQL 수정해야 됐음.  
- JPA: 필드만 추가하면 됨, SQL은 JPA가 처리함


<br>
<br>


## JPA가 패러다임의 불일치 해결
* 신뢰할 수 있는 엔티티, 계층
* 자유로운 객체 그래프 탐색 => 지연로딩

<br>

```java
Memeber member = memberDAO.find(memberID);
member.getTeam();
member.getOrder().getDelivery();
```

JPA에서 조회를 할 때, 동일한 트랜잭션에서 조회한 엔티티는 같음을 보장함.

<br>


## JPA의 성능 최적화 기능
- 1차 캐시와 동일성 보장
	- 같은 트랜잭션 안에서는 같은 엔티티를 반환 - 약간의 조회 성능 향상 
	- 메모리 상에서 반환해주기 때문에 SQL 한 번만 사용.

<br>

중간에 뭔가 기술이 끼게 되면, 두가지 성능상 이점을 가질 수 있는 찬스를 얻게 되는데 하나는 모아서 보내는 것이 가능함 => 버퍼 라이팅.
또 하나는, 캐싱. 이미 조회된 것은 멀리 안 가고 중간에서 있는 것을 다시 반환해줄 수 있는 기능.

<br>

- 트랜잭션을 지원하는 쓰기 지연 - INSERT
	- 트랜잭션을 커밋할 때까지 INSERT SQL을 모음
	- JDBC BATCH SQL기능을 사용해서 한번에 SQL 전송

<br>

```java
transaction.begin(); // 트랜잭션 시작
em.persist(memberA);
em.persist(memberB);
em.persist(memberC);
//여기까지 INSERT SQL을 데이터베이스에 보내지 않음

transaction.commit();
//커밋하는 순간 데이터베이스에 INSERT SQL을 모아서 보냄 => 이게 바로 버퍼 라이팅이 가능한 것.
```

<br>

- 트랜잭션을 지원하는 쓰기 지연 - UPDATE
- 지연 로딩과 즉시 로딩
	- 지연 로딩: 객체가 실제 사용될 때 로딩
	- 즉시 로딩: JOIN SQL로 한번에 연관된 객체까지 미리 조회

<br>
<br>

![image](https://github.com/Djangowon/TIL/blob/main/image/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202023-08-17%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%2012.19.29.png)

<br>

객체지향, 관계형 데이터베이스 두가지 개념을 잘 알아야 함

<br>
<br>


# JPA 실습

<br>

## 주의
- 엔티티 매니저 팩토리는 하나만 생성해서 애플리케이션 전체에서 공유  
- 엔티티 매니저는 쓰레드간에 절대 공유하면 안 됨(데이터베이스 커넥션을 사용하고 버리는 것처럼)  
- **JPA의 모든 데이터 변경을 트랜잭션 안에서 실행해야 됨  

<br>

## JPQL
> 테이블이 아닌 객체를 대상으로 검색하는 객체 지향 쿼리. 한마디로 정의하면 객체 지향 SQL

<br>


- JPA를 사용하면 엔티티 객체를 중심으로 개발함
- 문제는 검색 쿼리 (ex. JOIN)
- 검색을 할 때도 테이블이 아닌 엔티티 객체를 대상으로 검색쿼리를 짤 수 있는 문법이 들어가 있음
- 모든 DB 데이터를 객체로 변환해서 검색하는 것은 불가능함
- 애플리케이션이 필요한 데이터만 DB에서 불러오려면 결국 검색 조건이 포함된 SQL이 필요함

<br>

- JPA는 SQL을 추상화한 JPQL이라는 객체 지향 쿼리 언어를 제공함
- SQL과 문법 유사함
	> select, from, where, group by, having, join 지원
- JPQL은 엔티티 객체를 대상으로 쿼리
- SQL은 데이터베이스 테이블을 대상으로 쿼리



