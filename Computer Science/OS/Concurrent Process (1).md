# Concurrent Process
## 병행성(concurrency)
* 여러 개의 프로세스 또는 쓰레드가 동시에 실행되는 시스템의 특성

## 병행 프로세스(Concurrent Process)
* 동시에 실행되는 여러 개의 프로세스 또는 쓰레드

### 병행 프로세스의 실행 형태
* CPU의 개수에 따른 병행 프로세스의 실행 형태
    * 하나의 CPU에서 인터리빙 형식으로 실행
        > 인터리빙(interleaving): 하나를 잘개 쪼개서 계속 돌리면서 실행됨. 사전적 의미는 '끼워 넣기' 
    * 여러 개의 CPU에서 병렬 처리 형식으로 실행

### 병행 프로세스의 실행 형태 - 여러 개의 CPU
* 메모리 구조에 따른 병행 프로세스의 실행 형태
    * 강결합 멀티프로세서 시스템
        * 공유 메모리 구조

    * 약결합 멀티프로세서 시스템
        * 분산 메모리 구조

### 병행성 문제
* 병행 프로세스들이 상호작용 하는 경우 발생
    * 공유자원 점유 문제
    * 동기화 문제
    * 통신 문제

* 상황에 따른 구분
    * 단일 프로세스 내의 병행성
    * 프로세스 간의 병행성

## 단일 프로세스 내의 병행성
> `우선순위 그래프`, `Fork/Join 구조`, `병행문` 이라는 방식으로 단일 프로세스 내의 병행성 문제를 다뤄볼 수 있다.

### 우선순위 그래프
* 정점: 문장
* 방향 있는 간선: 우선순위 관계

### Fork/Join 구조
* fork L: 2개의 병행 수행을 만듦(레이블 L 위치, fork 명령어 다름)
* join n: 병행하는 n개의 흐름을 하나로 재결합

### 병행문
* I개의 프로세스가 여러 가닥의 병렬 프로세스로 분할되었다가 다시 하나로 결합
* parbegin / parend 문

### 프로세스 간의 병행성
* 비동기 병행 프로세스
    > 공유자원을 쓸 때 양쪽에서 동시에 작업을 할 경우, 데이터가 꼬이는 일이 발생할 가능성 있음 -> 이런 일이 발생하지 않기 위한 `동기화와 임계영역`

## 동기화와 임계영역
* 프로세스 동기화
    * 2개 이상의 프로세스에 대한 처리순서를 결정하는 것
    * ex) 동시에 사용할 수 없는 공유자원, 한 프로세스의 처리 결과에 따라 다른 프로세스의 처리가 영향을 받는 경우

* 임계영역
    * 2개 이상의 프로세스가 동시에 액세스하면 안 되는 공유자원을 액세스하는 코드 영역

* 상호배제
    * 2개 이상의 프로세스가 동시에 임계영역에 진입하지 못하도록 하는 것

### 임계영역 문제 해결을 위한 요구조건
* 상호배제
    * 한 프로세스가 임계영역에서 실행 중일 때 다른 어떤 프로세스도 임계영역에서 실행될 수 없음

* 진행
    * 임계영역에서 실행 중인 프로세스가 없고 여러 프로세스가 임계영역에 진입하고자 할 때 그 중에서 적절히 한 프로세스를 결정해야 하며 이 결정은 무한정 미룰 수 없음

* 제한된 대기
    * 한 프로세스가 임계영역 진입 요청을 한 후 수락될 때까지 다른 프로세스가 임계영역 진입을 허가 받는 횟수는 제한이 있어야 함

## 임계영역 문제 해결을 위한 도구
### Test-and-Set 명령어(TS명령어)
* 상호배제의 하드웨어적 해결 방법
* 분리가 불가능한 단일 기계 명령어(원자적으로 수행)
```
function Test_and_Set(var target: boolean): boolean;
    begin
        Test_and_Set:= target;
        target:= true;
    end
```
#### 상호배제의 구현
```
repeat
    while Test_and_Set(lock) do skip;
    임계영역
    lock:= false;
    잔류영역
until false;
```
#### 문제점
* 많은 프로세스가 임계영역에 들어가기를 원할 때 기아가 발생할 수 있음
    > 기아(starvation): 프로세스가 필요한 자원할당을 받지 못하고 계속적으로 대기하게 되는 상황
* Busy waiting을 함으로써 다른 작업이 사용할 수 있는 CPU 사이클을 

### 세마포어(semaphore)
* Dijkstra가 제안한 동기화 도구
* 세마포어 s: 사용 가능한 자원의 수 또는 잠김/열림 등의 상태를 나타내는 값을 저장하는 정수형 공용변수
* 세마포어 s는 두 표준단위 연산 p와 v에 의해서만 접근됨
    >  P(s): 검사, 감소시키려는 시도 / V(s): 증가

#### 상호배제의 구현
* 세마포어 mutex의 초깃값은 1
```
repeat
    P(mutex);
    임계영역
    V(mutex);
    잔류영역
until false;
```

### 동기화 문제 해결
* 프로세스 1이 문장 S₁을 실행한 후 프로세스 2가 문장 S₂를 실행하도록 동기화(block/wakeup 프로토콜)

#### 예시
```
# 프로토콜 1
S₁;
V(sync); # wakeup
```
```
# 프로토콜 2
P(sync); # block
S₂;
```
* 세마포어 sync의 초깃값은 0