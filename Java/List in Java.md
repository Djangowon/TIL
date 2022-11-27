# List

<br>
<br>

## array의 가장 큰 특징
> 메모리 상으로 연속되어서 구성됨, index 번호만 알면 접근 가능함

<br>

* 여러개의 데이터를 한꺼번에 다룰 수 있음
* array는 Object는 아니지만 Reference Value로 취급됨
* 메모리상에 연달아 공간을 확보함
* 미리 공간을 확보해놓고 써야 함
* 한 번 만들어진 공간은 크기가 고정됨
* 첫번째 위치만 알면 Index를 통해 상대적 위치를 빠르게 찾을 수 있음


<br>
<br>


## List
* Linked List
* Double Linked List(양방향)
* 여러개의 데이터를 한꺼번에 다룰 수 있음
* 메모리상에 연속되지 않아도 됨
* 미리 공간을 확보해놓지 않아도 됨
* 필요에 따라 데이터가 늘어나거나 줄어듬
* 첫 번째 위치로부터 index로 목표위치를 알려면 한 칸 한 칸 이동하면서(링크를 따라가면서) 찾아야 함


<br>
<br>


## Vector
* Vector는 synchronized 되어 있기 때문에 값을 추가하거나 삭제할 때 동기화 기능이 동작을 함
* 따라서, 추가/삭제할 경우에 synchronized 없이 동작하는 arrayList 보다는 좀 더 오버헤드가 있음
* 하지만, 멀티스레드 환경에서는 Vector를 사용해서 데이터의 정확성을 지켜주고 스레드를 safe하게 만드는 것이 더 유리함


<br>
<br>


* synchronized 필요없고, 멀티스레드 환경이 아니고, 스레드가 safe하지 않아도 된다? => arrayList 
* index로 빠르게 접근해야 한다면 => arrayList

