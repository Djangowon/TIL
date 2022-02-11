# Stack and Queue
## Stack
<img src="https://github.com/Djangowon/TIL/blob/main/image/stack.png" width=40% height=40%/>

* stack이란 쌓아 올린다는 것을 의미함
* 스택 자료구조라는 것은 책을 쌓는 것처럼 차곡차곡 쌓아 올린 형태의 자료구조를 말함
### Stack의 특징
* 같은 구조와 크기의 자료를 정해진 방향으로만 쌓을 수 있고, top으로 정한 곳을 통해서만 접근가능
* 스택에서 자료를 삭제할 때도 top을 통해서만 가능
    * 스택에서 top을 통해 삽입하는 연산을 `push`, top을 통한 삭제하는 연산을 `pop`이라고 함
* 따라서, 스택의 구조적 특징으로는 시간 순서에 따라 자료가 쌓여서 가장 마지막에 삽입된 자료가 가장 먼저 삭제된다고 할 수 있음
    * 이러한 스택의 구조를 `후입선출(LIFO, Last-In-First-Out) 구조` 라고 함
* 비어있는 스택에서 원소를 추출하려 할 때 stack underflow라고 하며, 스택이 넘치는 경우 stack overflow라고 한다. ("stack overflow " 의 이름이 여기서 유래 된 것!)
### Stack의 활용 사례
스택의 특징인  후입선출(LIFO)을 활용하여 여러 분야에서 활용 가능하다.
* 웹 브라우저 방문기록 (뒤로 가기) : 가장 나중에 열린 페이지부터 다시 보여준다.
* 역순 문자열 만들기 : 가장 나중에 입력된 문자부터 출력한다.
* 실행 취소 (undo) : 가장 나중에 실행된 것부터 실행을 취소한다.
* 후위 표기법 계산
* 수식의 괄호 검사 (연산자 우선순위 표현을 위한 괄호 검사)

## Queue
<img src="https://github.com/Djangowon/TIL/blob/main/image/queue.png" width=40% height=40%/>  

* 영어 단어 Queue는 표를 사러 일렬로 늘어선 사람들로 이루어진 줄을 의미함, 먼저 줄을 선 사람이 먼저 나갈 수 있는 상황을 연상하면 된다.
* Queue는 먼저 집어 넣은 데이터가 먼저 나오는 `FIFO(First-In-First-Out)구조`로 저장하는 형식을 말한다. 
* 나중에 집어 넣은 데이터가 먼저 나오는 스택과 반대되는 개념
### Queue의 특징
* 정해진 한 곳(top)을 통해서 삽입, 삭제가 이루어지는 스택과는 달리 큐는 한쪽 끝에서 삽입 작업이, 다른 쪽 끝에서 삭제 작업이 양쪽으로 이루어짐
   * 이때, 삭제연산만 이루어지는 곳을 `프론트(front)`, 삽입연산만 이루어지는 곳을 `리어(rear)`로 정하여 각각의 연산작업만 수행됨
   * 큐의 리어에서 이루어지는 삽입연산을 `인큐(enQueue)`, 프론트에서 이루어지는 삭제연산을 `디큐(dnQueue)`라고 부름
      * 큐의 가장 첫 원소를 front / 가장 끝 원소를 rear
      * 큐는 들어올 때 rear로 들어오지만 나올때는 front부터 빠지는 특성
      * 접근방법은 가장 첫 원소와 끝 원소로만 가능
      * 가장 먼저 들어온 프론트 원소가 가장 먼저 삭제  

즉, 큐에서 프론트 원소는 가장 먼저 큐에 들어왔던 첫 번째 원소가 되는 것이며, 리어 원소는 가장 늦게 큐에 들어온 마지막 원소가 되는 것이다.
### Queue의 활용 사례
큐는 주로 데이터가 입력된 시간 순서대로 처리해야 할 필요가 있는 상황에 이용한다.
* 우선순위가 같은 작업 예약 (프린터의 인쇄 대기열)
* 은행 업무
* 콜센터 고객 대기시간
* 프로세스 관리
* 너비 우선 탐색(BFS, Breadth-First Search) 구현
* 캐시(Cache) 구현

## Code로 구현해보기
### Stack
```python
## Stack Class

class Stack:
    def __init__(self): # 스택 객체 생성
        self.items = []

    def push(self, item): # 스택 요소 추가 push(.append())
        self.items.append(item)

    def pop(self): # 스택 요소 삭제 pop()
        return self.items.pop()

    def peek(self): # 스택 맨 앞 요소 리턴
        return self.items[0]

    def isEmpty(self): # 스택이 비었는지 확인(비었으면 True 리턴)
        return not self.items


stk = Stack() # 스택 객체 생성
print(stk) # 스택 오브젝트 생성 확인
# => <__main__.Stack object at 0x7f85f00b2f10> : 생성됨
print(stk.isEmpty()) # 처음에는 아무것도 들어있지 않으므로 True 반환
stk.push(1) # stk 에 1 삽입 : [1]
stk.push(2) # stk 에 2 삽입 : [1,2]
stk.push(3) # stk 에 3 삽입 : [1,2,3]
print(stk.items) # => [1,2,3]
print(stk.pop()) # stk 에 3이 꺼내지면서 출력 : 3 / [1,2]
print(stk.peek()) # stk 맨 앞 값 출력 : 1
print(stk.isEmpty()) # 비어있지 않으므로 False 출력
print(stk.pop()) # stk 에 2이 꺼내지면서 출력 : 2 / [1]
print(stk.pop()) # stk 에 1이 꺼내지면서 출력 : 1 / []
print(stk.isEmpty()) # 객체에 아무것도 들어있지 않으므로 True 반환
```
### Queue
```python
import queue

# Queue 선언
q = queue.Queue()

# q에 데이터 추가
q.put(1)
q.put(2)
q.put(3)
q.put(4)

# q에서 첫번째 원소 제거
print(q.get()) # 1
print(q.get()) # 2
print(q.get()) # 2
print(q.get()) # 4


from collections import deque


class Queue(deque):
    def enqueue(self, x):
        super().append(x)

    def dequeue(self):
        super().popleft()

    def display(self):
        for node in self.__iter__():
            print(node)


qu = Queue()
print(qu)
qu.enqueue(1)
qu.enqueue(2)
qu.enqueue(3)
print(qu)
qu.dequeue()
print(qu)
qu.display()
```

[Ref](https://devuna.tistory.com/22/)  
[Ref](https://gorokke.tistory.com/129/)  
[Ref](https://daimhada.tistory.com/107/)
