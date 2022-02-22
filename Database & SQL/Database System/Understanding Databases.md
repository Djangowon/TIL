# Understanding Databases
## 데이터베이스의 역할
### 데이터 단위
|바이트|1Byte|8bit|
|:---|:---|:---|
|킬로바이트|1KiloByte|1024Byte|
|메가바이트|1MegaByte|1024KB|
|기가바이트|1GigaByte|1024MB|
|테라바이트|1TeraByte|1024GB|
|페타바이트|1PetaByte|1024TB|
|엑사바이트|1ExaByte|1024PB|
|제타바이트|1ZetaByte|1024EB|
|요타바이트|1YottaByte|1024ZB|

### 빅데이터 처리
<img src="https://github.com/Djangowon/TIL/blob/main/image/en_lpwa_img_1.png" height=40% width=40%>

### 데이터 관리의 필요
#### 데이터 관리 장치란?
* 대량의 데이터를 저장 및 관리하고 필요한 데이터를 신속히 검색할 수 있도록 보조하는 장치

### 데이터 관리의 역사
#### 전통적 데이터 관리 방식
* 파일 처리 시스템(file processing system)
    * 데이터베이스가 개발되기 전에 데이터 관리에 사용
    * 업무 별 애플리케이션이 개별 데이터를 데이터 파일에 저장,관리하는 시스템
    * 발생 가능한 문제
        * 데이터 종속의 문제
            * 저장된 데이터가 특정 H/W에서 또는 사용자 및 S/W만 사용될 수 있도록 제한되는 문제
                * 물리적 데이터 종속
                * 논리적 데이터 종속
        * 데이터 중복의 문제
            * 동일한 사항에 대한 중복 데이터는 일관성, 보안성, 경제성 측면에서 문제 발생
                * 일관성: 한 사실에 대해 한 개의 데이터 값을 유지
                * 보안성: 같은 데이터에 같은 수준의 보안 유지
                * 경제성: 데이터에 대해 최소한의 저장 공간 만을 점유
        * 무결성 훼손의 문제
            * 실세계의 데이터는 데이터가 가질 수 있는 가능 범위(제약조건)를 포함
                * 현상에 대한 값의 예: '홍길동'의 수강과목
                * 가능 범위의 예: 1학기 최대 수강과목 18학점
            * 데이터 무결성
                * 데이터의 정확성 보장
                * 데이터의 값과 값에 대한 제약조건을 동시에 만족
            * 파일 시스템은 데이터 무결성을 보장하기 위한 기능을 제공하지 않음
        * 동시 접근의 문제
            * 동일 데이터에 다수 사용자의 접근 허용 시 일관성이 훼손

## 데이터베이스의 특징
* 데이터베이스 시스템의 자기 기술성
    * 데이터와 데이터의 정의 및 설명(메타데이터)을 포함
* 프로그램과 데이터의 격리 및 추상화
    * 사용자에게 데이터에 대한 개념적인 표현을 제공하여 접근성을 향상
* 다중 뷰 제공
    * 각 사용자가 관심을 갖는 데이터베이스의 일부만을 표현할 수 있는 기능 제공
* 데이터 공유와 다수 사용자 트랜잭션 처리
    * 다수의 데이터 조작 요청을 동시성 제어 기능을 통해 데이터의 일관성을 보장하면서 동시에 작업을 수행

### 데이터베이스 시스템의 구성
#### DBMS의 3단계 구조
<img src="https://github.com/Djangowon/TIL/blob/main/image/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202022-02-22%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%208.13.20.png" height=70% width=70%>

* 개념단계: 어떤 의미의 어떤 구조의 데이터가 있는지만을 표현함
* 내부단계: 실제 하드웨어를 관리하는 사람 입장에서는 내부단계에서 어떤 데이터가 어디에 저장되는지 알 필요가 있음
* 외부단계: 실제 데이터를 사용하는 사람이 개념과 내부단계의 데이터 의미, 물리적 구조를 알 필요없이 실제 데이터를 그대로 사용할 수 있게끔 하는 레이어(껍데기)라고 할 수 있음
> DBMS는 데이터의 추상화를 위해 외부-개념-내부 3단계로 구조화되며 외부-개념 사상 과정에서 논리적 데이터 독립성, 개념-내부 사상을 통해 물리적 데이터 독립성이 확보된다.

### 다수 사용자 트랜잭션 처리
#### 트랜잭션의 정의
* 하나의 논리적 작업을 처리하기 위한 일련의 데이터베이스 명령의 집합

### 데이터베이스 관련 용어
* 데이터(data): 어떠한 사실에 대한 정량적, 정서적 특징을 나타낼 수 있는 값과 값에 대한 설명
* 데이터베이스(database): 특정 기관의 애플리케이션 시스템에서 사용되는 데이터의 집합
* 데이터베이스 관리 시스템(DBMS): 데이터베이스에 저장된 데이터의 구성, 저장, 관리, 사용을 위한 소프트웨어 패키지
* 데이터베이스 시스템(database system): 정보를 데이터베이스에 저장, 관리하여 사용자에게 요구된 형태의 정보로 제공하는 컴퓨터 기반 시스템

## 데이터베이스의 구성요소
### 데이터베이스 언어
* DBMS는 사용자가 데이터베이스를 쉽게 사용하고 다룰 수 있도록 언어 형태의 인터페이스를 제공
* 역할에 따라 종류의 언어로 구분
    * 데이터 정의 언어(DDL)
        * DDL: Data Definition Language
        * 데이터베이스 객체를 생성, 수정, 삭제하기 위한 언어
        * DDL의 요구 기능
            * 데이터 모델에 따라 애플리케이션 프로그램이 요구하는 데이터의 논리적 구성이나 특징을 규정
            * 데이터가 기억장치에 저장되도록 데이터의 물리적 구성을 규정
            * 물리적 구성을 논리적 구성으로 변환이 가능하도록 데이터의 물리적 구성과 논리적 구성 간의 사상을 규정
    * 데이터 조작 언어(DML)
        * DML: Data Manipulation Language
        * 구조화된 데이터에 사용자가 접근 및 조작할 수 있도록 지원하는 언어(검색, 삽입, 삭제, 수정)
        * DML의 요구 조건
            * 데이터 조작이 쉽고 간편
            * 데이터 조작 기능이 정확하고 완전
            * 사용자의 요청을 시스템 내부에서 효율적으로 처리 가능
* 현대 데이터베이스 언어는 자연어와 유사한 형태의 SQL로 표준화

### 데이터베이스 시스템 아키텍처
#### 중앙집중식 방식
* 단일 서버가 다수의 클라이언트 장치를 대신하여 작동
* 중앙 컴퓨터의 과부하로 전체적인 성능 저하
* 저렴하게 시스템을 구성할 수 있지만, 중앙에 일이 몰려서 일이 쌓이면 전체 시스템이 모두 한꺼번에 느려지는 단점이 있는 아키텍처

#### 분산 시스템 방식
* 클라이언트 장치의 성능 향상으로 자체적인 처리 능력 보유
* 클라이언트-서버 데이터베이스 시스템
    * 애플리케이션 프로그램의 부하를 분산
    * 소프트웨어의 유지보수 비용을 절감 및 이식성 증가