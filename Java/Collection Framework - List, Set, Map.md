# Collection Framework - List, Set, Map

<br>
<br>


## Collection Framework
* 다수의 데이터를 쉽고 효과적으로 처리할 수 있는 표준화된 방법을 제공하는 클래스의 집합을 의미함
* 데이터를 저장하는 자료 구조와 데이터를 처리하는 알고리즘을 구조화하여 클래스로 구현해 놓은 것
* 자바의 인터페이스를 사용하여 구현됨


<br>

* 컬렉션 프레임워크의 주요 인터페이스 3가지 특징


|인터페이스|설명|구현 클래스|
|:---:|:---:|:---:|
|List\<E\>|순서 있음, 데이터 중복 허용|Vector, ArrayList, LinkedList, Stack, Queue|
|Set\<E\>|순서 없음, 데이터 중복 불가|HashSet, TreeSet|
|Map<K, V>|키, 값 형태의 데이터 집합. 순서 없음, 키는 중복 불가. 값은 중복 허용|HashMap, TreeMap, Hashtable, Properties|

<br>
<br>


## Iterator
* 컬렉션에 저장된 요소를 읽어오는 방법
* 배열 등의 자료구조 안을 돌면서 들어있는 데이터에 접근할 수 있게 해주는 객체


<br>
<br>


## Iterator의 장점

* 컬렉션에서 요소를 제어할 수 있음
* 자료구조를 돌다가 값을 수정, 삭제하는 등의 for-each 반복문이 할 수 없는 일을 할 수 있음
    > 예를 들어, 리스트에는 인덱스가 있지만 순서가 없는 Set은 인덱스가 없기 때문에 일반 for문을 사용할 수 없지만, for-each문은 사용할 수 있음  
    > for-each문으로 자료구조를 돌다가 값을 수정, 삭제해야 해서 수정, 삭제를 수행하는 코드를 넣으면 ConcurrentModificationException이 발생함  
* 양방향으로 반복할 수 있음
* next() 및 previous()를 써서 앞뒤로 이동 가능
* hasNext()를 써서 더 많은 요소가 있는지 확인 가능


<br>
<br>


## List 컬렉션 클래스

1. ArrayList\<E\>
2. LinkedList\<E\>
3. Vector\<E\>
4. Stack\<E\>

<br>


```java
        // 컬렉션 생성
        List<String> al = new ArrayList<String>();
        al.add("레몬차");
        al.add("블루베리 스무디");
        al.add("자몽허니 블랙티");
        al.add("청귤차");

        // iterator 획득
        ListIterator<String> listIterator = al.listIterator();

        // while문 사용
        while(listIterator.hasNext())
        {
            String str = listIterator.next();
            System.out.println(str);
        }

        // for-each문 사용 (Enhanced for 문), 리스트에서는 JDK 1.5부터 추가된 Enhanced for 문을 사용 권장
        for (String str : al) {
            System.out.println(str);
        }

        // iterator 사용하여 반복문 돌며 수정
        while(listIterator.hasNext())
        {
            String str = listIterator.next();
            listIterator.set(str + "1111");
        }
        System.out.println("수정 후 : " + al);

        //역순 반복
        while(listIterator.hasPrevious())
        {
            Object element = listIterator.previous();
            System.out.print(element + " ");
        }

```
<br>
<br>


## Set 컬렉션 클래스
1. HashSet\<E\>
2. TreeSet\<E\>

<br>
<br>

## Map 컬렉션 클래스
1. HashMap<K, V>
2. Hashtable<K, V>
3. TreeMap<K, V>

<br>

```java
        Map<String, Integer> hm = new HashMap<>();

        hm.put("일",1);
        hm.put("이",2);
        hm.put("삼",3);

        
        for (String key: hm.keySet()) {
            System.out.println(key);
        }
```
> Map도 Set과 마찬가지로 순서가 없기 때문에 출력해보면 순서대로 안 나옴


<br>
<br>


## Ref
http://www.tcpschool.com/java/java_collectionFramework_concept  
http://www.tcpschool.com/java/java_collectionFramework_iterator  
https://onlyfor-me-blog.tistory.com/319  
http://www.tcpschool.com/java/java_collectionFramework_list  
http://www.tcpschool.com/java/java_collectionFramework_set  
http://www.tcpschool.com/java/java_collectionFramework_map  
