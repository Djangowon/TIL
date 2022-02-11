# Tree
* 트리는 가계도와 같은 계층적인 구조를 표현할 때 사용할 수 있는 자료구조임
<img src="https://github.com/Djangowon/TIL/blob/main/image/tree.png" height=90% width=90%>


### 트리 관련 용어
* 루트 노드(root node): 부모가 없는 최상위 노드
* 단말 노드(leaf node): 자식이 없는 노드
* 크기(size): 트리에 포함된 모드 노드의 개수
* 깊이(depth): 루트 노드부터의 거리
* 높이(height): 깊이 중 최댓값
* 차수(degree): 각 노드의 (자식 방향) 간선 개수

기본적으로 트리의 크기가 N일 때(즉, 트리에 포함되어 있는 노드의 개수가 N개 일 때), 전체 간선의 개수는 N-1개 이다.

## Binary Search Tree(이진 탐색 트리)
<img src="https://github.com/Djangowon/TIL/blob/main/image/binary-search-tree.png" height=90% width=90%>


* 이진 탐색이 동작할 수 있도록 고안된 효율적인 탐색이 가능한 자료구조의 일종
* 이진 탐색 트리의 특징: 왼쪽 자식 노드 < 부모 노드 < 오른쪽 자식 노드
    * 부모 노드보다 왼쪽 자식 노드가 작다.
    * 부모 노드보다 오른쪽 자식 노드가 크다.
### 이진 탐색 트리로 데이터를 조회하는 과정
* 루트 노드부터 방문하여 탐색을 진행
    * 현재 노드와 찾는 원소를 비교
      * 찾는 원소가 더 크면 오른쪽, 찾는 원소가 더 작으면 왼쪽 방문
        * 현재 노드와 값을 비교
          * 원소를 찾으면 탐색 종료
## Tree Traversal(트리의 순회)
* 트리 자료구조에 포함된 노드를 특정한 방법으로 한 번씩 방문하는 방법을 의미함
    * 트리의 정보를 시각적으로 확인가능
### 대표적인 트리 순회 방법
* 전위 순회(pre-order traverse): 루트를 먼저 방문한다.
* 중위 순회(in-order traverse): 왼쪽 자식을 방문한 뒤에 루트를 방문한다.
* 후위 순회(post-order traverse): 오른쪽 자식을 방문한 뒤에 루트를 방문한다.
