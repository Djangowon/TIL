# Inheritance Mapping - Joined, SingleTable, TablePerClass

<br>
<br>


## 상속관계 매핑
> 관계형 데이터베이스는 객체처럼 상속 관계가 없음, 슈터파입 서브타입 관계라는 모델링 기법이 객체의 상속과 유사함
* 상속관계 매핑: 객체의 상속과 구조와 DB의 슈퍼타입 서브타입 관계를 매핑


<br>
<br>

## 조인전략
```java
@Inheritance(strategy = InheritanceType.JOINED)
@DiscriminatorColumn
```
* 조인 전략이 객체와 가장 잘 맞고, 정규화도 되고, 설계 입장에서 가장 깔끔한 전략임
* 장점
	* 테이블이 정규화 되어있음
	* 외래 키 참조 무결성 제약조건 활용가능
	* 저장공간 효율화됨
* 단점
	* 조회시 조인을 많이 사용하기 때문에 성능저하
	* 조회 쿼리가 복잡함
	* 데티어 저장시 INSERT SQL 쿼리 2번 호출함
	> 조인을 많이 사용하거나 INSERT 쿼리가 두번 호출되는 것 등의 단점은 그렇게 크리티컬한 단점은 아님, 단일 테이블 전략에 비해 복잡하고 성능이 안 나올 가능성이 있음 


<br>
<br>


## 단일 테이블 전략
```java
@Inheritance(strategy = InheritanceType.SINGLE_TABLE)
@DiscriminatorColumn
```
* DTYPE이 필수로 생성됨
* 장점
	* 조인이 필요 없으므로 일반적으로 조회 성능이 빠름
	* 조회 쿼리가 단순함
* 단점
	* 자식 엔티티가 매핑한 컬럼은 모두 null 허용해야 함
	* 단일 테이블에 모든 것을 저장하므로 테이블이 커질 수 있고, 상황에 따라 조회 성능이 오히려 느려질 수 있음


<br>
<br>


## 구현 클래스마다 테이블 전략
```java
@Inheritance(strategy = InheritanceType.TABLE_PER_CLASS)
```
* 이 전략은 데이터베이스 설계자와 ORM 전문가 둘 다 추천하지 않음, 사용하지 말 것!
* 단순하게 값을 넣고 뺄 땐 좋은 것 같지만, 망하는 이유
	> JPA는 명확하게 하나를 조회할 땐 괜찮지만, 그 외의 경우 부모 클래스 타입으로 조회한다면 union all 을 사용해서 테이블을 다 뒤져봐야 하기 때문에 복잡한 쿼리가 나가게 됨.
	
* 장점
	* 서브 타입을 명확하게 구분해서 처리할 때 효과적임
	* not null 제약조건 사용 가능
* 단점
	* 여러 자식 테이블을 함께 조회할 때 성능이 느림(UNION SQL)
	* 자식 테이블을 통합해서 쿼리하기 어려움


<br>
<br>

## Ref
https://www.inflearn.com/course/ORM-JPA-Basic
