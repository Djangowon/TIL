# Array vs Linked List
## Array
* array는 논리적 저장순서와 물리적 저장 순서가 일치한다.
* random access가 가능하다.
    *  인덱스(index)로 해당 원소(element)에 접근할 수 있다.
    *  찾고자 하는 원소의 인덱스 값을 알고 있으면 Big-O(1)에 해당 원소로 접근할 수 있다.
* 배열의 원소를 삭제할 경우 삭제한 원소보다 큰 인덱스를 가진 원소들을 옮겨줘야(Shift) 하기 때문에 시간 복잡도 O(n)이 걸린다.
* 삽입의 경우, 새로운 원소를 추가하고 모든 원소들의 인덱스를 1씩 Shift 해줘야 하므로 시간 복잡도 O(n)이 걸린다.
* 제한적인 크기를 갖는다.

즉, 삭제 또는 삽입 과정에서 해당 원소에 접근하여 작업을 완료한 뒤 Shift를 해줘야 하는 cost가 발생해 O(n)의 time complexity를 갖는다.

## Linked List
* Array 와는 달리 논리적 저장 순서와 물리적 저장 순서가 일치하지 않는다.
    * 일단 삽입하고 정렬하는 것과 마찬가지
* 자료의 주소 값으로 노드를 이용해 서로 연결되어 있는 구조를 갖는다.
* 삽입과 삭제를 위해서 해당 노드를 찾아가는 동안 O(n)의 시간 복잡도를 갖는다. 
    * Search 과정에 있어서 첫번째 원소부터 다 확인해야 하기 때문
    * 추가적으로 데이터를 삽입 / 삭제하기 위한 시간 복잡도까지 계산하면 결국 O(n)의 시간 복잡도를 갖는 셈이다.
* 각각의 원소들은 자기 자신 다음에 어떤 원소인지만을 기억하고 있다.
    * 따라서 이 부분만 다른 값으로 바꿔주면 삭제와 삽입을 O(1) 만에 해결할 수 있는 것이다.
        * 삽입의 경우  
            일단, LinkedList는 어느 곳에 삽입하던지 O(n)의 시간복잡도를 갖는다. (만약, 중간 삽입이 없다면 즉 맨 앞과 맨 뒤에만 삽입한다면 -> 시간 복잡도 : O(1))
        * 삭제의 경우  
            삭제의 경우도 삽입과 마찬가지이다. 어느 곳에 삽입하던지 O(n)의 시간 복잡도를 갖는다. (만약, 중간 삭제가 없고 맨 앞과 뒤에서만 삭제한다면 -> 시간 복잡도 : O(1))
* 트리의 근간이 되는 자료구조이다.
    * Tree 에서 사용되었을 때 그 유용성이 드러난다.

결국 linked list 자료구조는 search 에도 O(n)의 time complexity 를 갖고, 삽입, 삭제에 대해서도 O(n)의 time complexity를 갖는다.

## Array vs Linked List
|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|Array|Linked List|
|:---:|:---|:---|
|데이터 접근속도| Random Access / 시간 복잡도 O(1)| 순차 접근 방식 / 시간 복잡도 O(N)|
|데이터 삽입속도| * 데이터를 중간이나 맨 앞에 삽입할 경우 그 이후의 데이터를 한 칸씩 미뤄야 하는 추가 과정과 시간이 소요된다. </br> * 데이터가 많을 경우 비효율적이다. 그렇기 때문에 LinkedList가 필요하게 되었다.| * 어느 곳에 삽입하던지 O(N)의 시간 복잡도를 갖는다.(만약, 중간 삽입이 없다면 O(1)의 시간복잡도를 갖는다.) </br> * 이유는 삽입할 위치를 찾고(O(N)) 삽입 연산을 진행하기 때문에 O(N)의 시간 복잡도를 갖는다. </br> * 그럼에도 Array보다 빠른 성능을 보인다.|
|메모리 공간| * 데이터 삽입 시 모든 공간이 다 차버렸다면 새로운 메모리 공간을 할당받는다. </br> * Array에서 메모리는 Array가 선언되자 마자 Compile time에 할당되어 진다. 이것을 정적 메모리 할당이라고 한다. </br> * Stack 영역에 메모리 할당이 이루어진다.| * 새로운 메모리 공간을 할당받을 필요 없이 추가할 때마다 동적으로 할당한다. </br> * LinkedList에서 메모리는 새로운 node가 추가될 때 runtime에 할당되어 진다. 이것은 동적 메모리 할당이라고 한다. </br> * Heap 영역에 메모리 할당이 이루어진다.|
|데이터 삭제속도| * 데이터 삭제의 경우 그 위치의 데이터를 삭제 후, 전체적으로 Shift 해줘야 한다. (O(N))| * LinkedList의 경우 삭제할 원소를 찾기 위해서 O(N)의 시간 복잡도를 갖고 삭제를 한다. 결국 O(N)의 시간 복잡도를 갖는다. </br> * 하지만 Array 보다 빠르게 삭제 연산을 수행한다.|

## 정리
* 삽입과 삭제가 빈번하다면 LinkedList를 사용하는 것이 더 좋다.
* 데이터의 접근하는 게 중요하다면 Array를 사용하는 것이 좋다.

[Ref](https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/DataStructure#array-vs-linked-list/)  
[Ref](https://woovictory.github.io/2018/12/27/DataStructure-Diff-of-Array-LinkedList/)
