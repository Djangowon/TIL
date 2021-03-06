# Divide-and-conquer algorithm
## 분할정복 방법의 원리
### 분할정복 방법(divide-and-conquer method)
* 순환적으로 recursively 문제를 푸는 하향식 top-down 접근 방법
    * 주어진 문제의 입력을 더 이상 나눌 수 없을 때까지 두 개 이상의 작은 문제로 순환적으로 분할하고,
    * 이렇게 분할된 작은 문제들을 각각 해결한 후, 이 해들을 결합해서 원래 문제의 해를 구하는 방식

* 특징
    * 분할된 작은 문제는 원래 문제와 동일
        * 단, 입력 크기만 작아짐
    * 분할된 작은 문제는 서로 독립적
        * 순환적 분할 및 결과 통합이 가능

### 분할정복 방법의 처리 단계
* 각 순환 호출마다 세 단계의 처리 과정을 거침
    * `분할`
        * 주어진 문제를 여러 개의 작은 문제로 분할한다.
    * `정복`
        * 작은 문제를 순환적으로 분할.
        * 만약 작은 문제가 더 이상 분할되지 않을 정도로 크기가 충분히 작다면 순환호출 없이 작은 문제의 해를 구한다.
    * `결합`
        * 작은 문제에 대해 정복된 해를 결합하여 원래 문제의 해를 구한다.  
            ** 결합 단계가 없는 문제도 존재

### 적용 알고리즘의 종류 및 분할 과정
<img src="https://github.com/Djangowon/TIL/blob/main/image/divide-and-conquer%20algorithm.png" height=60% width=60%>

## 이진 탐색
### 개념과 원리
* `정렬된 상태의 입력 데이터`에 대한 효과적인 탐색 방법
    * 오름차순으로 정렬되었다고 가정

* 탐색 방법
    * 배열의 가운데 원소 A[mid]와 탐색키 x를 비교
        * (1) 탐색키 = 가운데 원소 -> 탐색 성공(인덱스 mid 반환 후 종료)
        * (2) 탐색키 < 가운데 원소 -> `이진 탐색(원래 크기 ½인 왼쪽 부분배열` 순환 호출
        * (3) 탐색키 > 가운데 원소 -> `이진 탐색(원래 크기 ½인 오른쪽 부분배열` 순환 호출

        > 탐색을 반복할 때마다 대상 원소의 개수가 ½씩 감소 

|개념|원리|
|:---:|:---|
|`분할`|배열의 가운데 원소를 기준으로 왼쪽과 오른쪽 부분배열로 분할. </br>탐색키와 가운데 원소가 같으면 가운데 원소의 배열 인덱스를 반환/종료|
|`정복`|탐색키가 가운데 원소보다 작으면 왼쪽 부분배열을 대상으로 이진 탐색을 순환 호출, </br>크면 오른쪽 부분배열을 대상으로 이진 탐색을 순환 호출|
|`결합`|필요 없음(부분 배열에 대해서 탐색 결과가 직접 반환)|

### 성능 분석
* T(n) = 입력 크기 n에 대한 탐색 과정에서의 모든 비교 횟수의 합 = 맨 바깥 수준에서의 비교 횟수 + 순환 호출에서의 비교 횟수
    > T(n) = T(n/2) + O(1) (n>1), T(1) = 1
    > > T(n) = O(logn)

### 특징
* 입력 배열의 데이터가 정렬된 경우에 대해서만 적용 가능
* 삽입/삭제 연산은 부가적인 데이터 이동을 수반
    * 데이터의 정렬 상태 유지를 위해서 평균 n/2개의 데이터 이동이 발생
        * 삽입/삭제가 빈번한 응용에서는 부적합

## 퀵 정렬
* `특정 원소`를 기준으로 주어진 배열을 두 부분배열로 분할하고, 각 부분배열에 대해서 퀵 정렬을 순환적으로 적용하는 방식
    * 오름차순으로 정렬한다고 가정

* 피벗(pivot)
    * 주어진 배열을 두 부분배열로 분할할 때 기준이 되는 특정 원소
        * 보통 주어진 배열의 첫 번째 원소로 지정

* 피벗이 제자리를 잡도록 하여 정렬하는 방식
    > 왼쪽 부분배열의 모든 값 < `피벗` < 오른쪽 부분배열의 모든 값

|개념|원리|
|:---:|:---|
|`분할`|피벗을 기준으로 주어진 배열을 두 부분배열로 분할한다.|
|`정복`|두 부분배열에 대해서 퀵 정렬을 순환적으로 적용하여 각 부분배열을 정렬한다.|
|`결합`|필요 없음|

### 성능 분석
* 분할 함수 Partition() 수행 시간
    * 피벗과의 비교 횟수
        > Θ(n) / O(n)

* 퀵 정렬 QuickSort() 수행 시간
        > T(n) = T(a) + T(b) + Θ(n) (n>1)
        > > T(1) = Θ(1)
        > > 
    * 분할된 두 부분배열의 크기에 따라서 성능 시간이 달라진다.

#### 성능 분석_최악의 경우
* 배열이 항상 0:n-1 또는 n-1:0으로 분할되는 경우
    * 극심한 불균형적 분할 
        * 0:n-1, n-1:0 ->피벗만 제자리를 잡고 나머지 모든 원소가 하나의 부분배열이 되는 경우
        * 피벗이 항상 부분배열의 최솟값 또는 최댓값이 되는 경우
        * 입력 데이터가 정렬된 경우 AND 피벗을 배열의 처음 원소를 정한 경우
        > T(n) = T(n-1) + T(0) + Θ(n) (n>0), T(0)=0
        > > T(n) = T(n-1) + Θ(n)
        > > > T(n) = O(n²)

#### 성능 분석_최선의 경우
* 배열이 항상 n/2:n/2로 분할되는 경우
    * 가장 균형적인 분할
        * 피벗을 중심으로 항상 동일한 크기의 두 부분배열로 분할되는 경우
        * 피벗이 항상 부분배열의 중간값이 되는 경우
        > T(n) = T(⎣n/2⎦) + T(⎣n/2⎦) + Θ(n) (n>1), T(1)=1
        > > T(n) = 2T(n/2) + Θ(n)
        > > > T(n) = O(nlogn)

#### 성능 분석_평균적인 경우
* 부분배열의 모든 분할 비율에 따른 수행 시간의 평균
    * 피벗은 동일한 확률로서 분할 수 배열의 어느 곳에나 위치 가능
        > <img src="https://github.com/Djangowon/TIL/blob/main/image/quicksort_exam.png" height=50% width=50%>
        > > T(n) = O(nlogn)

### 특징
* 최선/평균 수행 시간 -> O(nlogn)
* 최악 수행 시간 -> O(n²)
    * 피벗 선택의 임의성만 보장되면 평균 성능을 보일 가능성이 매우 높음
        * 배열에서 임의의 값을 선택한 후, 배열의 처음 원소와 서로 교환한 후 정렬 수행

## 합병 정렬
* 전형적인 분할정복 방법이 적용된 알고리즘

|개념|원리|
|:---:|:---|
|`분할`|배열을 동일한 크기의 두 개의 부분배열로 분할하고,|
|`정복`|각각의 부분배열을 순환적으로 정렬한 후,|
|`결합`|정렬된 두 부분배열을 합병하여 하나의 정렬된 배열을 만듦|

### 성능 분석
* 합병 함수 Merge() 수행 시간
    * 입력 데이터 개수 n만큼의 추가 저장 장소 (B[]+C[])가 필요
        > 이런 경우, `제자리 정렬 알고리즘`이 아니다.

* 합병 정렬 MergeSort() 수행 시간
    > T(n) = T(⎣n/2⎦) + T(⎣n/2⎦) + Θ(n) (n>1), T(1)=1
    > > T(n) = 2T(n/2) + Θ(n)
    > > > T(n) = O(nlogn)

### 비순환적 합병 정렬
* 합병만 반복적으로 수행해서 합병 정렬을 수행하는 것도 가능함

## 선택 문제
* n개의 원소가 임의의 순서로 저장된 배열 A[0..n-1]에서 i번째로 작은 원소를 찾는 문제

* 직관적인 방법
    * 오름차순으로 정렬한 후 i번째 원소를 찾는 방법 -> O(nlogn)
    * 최솟값을 찾는 과정을 i번 반복(i-1번째까지는 최솟값을 찾은 후 삭제) -> O(in) / O(n²)

### 최솟값 찾기
* 각 데이터를 하나씩 모두 비교하는 방법
    * n개의 데이터에 대해서 적어도 (n-1)번의 비교가 필요 -> O(n)

### 최솟값과 최댓값 모두 찾기
* 방법1: 최솟값 찾은 후 최댓값 찾기(or 최댓값 찾은 후 최솟값 찾기)
    * n개의 데이터에서 최솟값을 찾는데 (n-1)번 비교
    * (n-1)개의 데이터에서 최댓값을 찾는데 (n-2)번 비교
    * 2n-3번의 비교 -> O(n)

* 방법2: 모든 원소를 두 개씩 짝을 이루어 동시에 최솟값/최댓값과 비교
    * 3/2n-2번의 비교

### i번째로 작은 원소 찾기_최악 O(n²), 평균 O(n)
* 퀵 정렬의 분할 함수 Partition()을 순환적으로 적용하는 방법

|개념|원리|
|:---:|:---|
|`분할`|피벗을 기준으로 주어진 배열을 두 부분배열로 분할하고, i가 피벗의 인덱스 p와 같으면 피벗의 값을 반환하고 종료|
|`정복`|인덱스 i가 포함된 부분배열에 대해서 알고리즘을 순환적으로 호출하여 적용|
|`결합`|필요 없음|

### 성능 분석
* 최악의 경우 = 퀵 정렬의 최악의 경우
    * 분할 함수 Partition()이 항상 하나의 부분배열만 생성하는 경우
    * 오름차순을 정렬된 상태에서 최댓값(i=n)을 찾는 경우
        * 분할 함수를 호출할 때마다 피벗 인덱스는 1씩 증가
        * Partition()를 O(n)번 호출 => O(n²)
            > Partition() = O(n)
    * 해결방법 -> 항상 일정한 비율의 두 부분배열로 분할 -> 최악의 경우에도 O(n)

* 평균적인 경우 -> O(n)

### i번째로 작은 원소 찾기_최악 O(n), 평균 O(n)
* 항상 일정한 비율의 두 부분배열로 분할되도록 특정 성질을 만족하는 값을 피벗으로 선택

* 피벗 선택 방법
(1) 크기 n인 배열의 원소를 5개씩 묶어서 ⎣n/5⎦개의 그룹을 만듦
    * 5의 배수가 되지 않아 그룹을 형성하지 못한 채 남는 원소는 그대로 남겨 둠
(2) 각 그룹에 대해서 중간값을 찾음
(3) ⎣n/5⎦개의 중간값을 대상으로 다시 중간값을 찾음
    -> 중간값들의 중간값 -> `피벗`

### 간단 정리
* 합병 정렬: 크기가 n인 문제를 크키가 n/2인 두 개의 작은 문제로 분할
* 이진 탐색: 크기가 n인 문제를 크기가 n/2인 두 개의 작은 무제로 분할하고, 그 중 하나의 작은 문제는 처리 대상에서 제외
* 선택 문제: 크기가 n인 문제를 일정하지 않은 크기를 갖는 두 개의 작은 문제로 분할하고, 그 중 하나의 작은 문제는 처리 대상에서 제외
* 퀵 정렬: 크기가 n인 문제를 일정하지 않은 크기를 갖는 두 개의 작은 문제로 분할
