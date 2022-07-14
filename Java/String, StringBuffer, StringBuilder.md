# String, StringBuffer, StringBuilder

<br>
<br>

> Java에서 문자열을 다루는 대표적인 클래스로 String, StringBuffer, StringBuilder가 있음

<br>

## String
* String과 StringBuffer/StringBuilder 클래스의 가장 큰 차이점은 String은 불변(immutable)의 속성을 갖는다는 점임

```java
String str = "안녕"; // String str = new String("안녕");
str = str + "하세요?"; // 
```
* 위의 코드처럼 str을 수정하려고 한다면, 기존에 "안녕"값이 들어있던 String 클래스의 참조변수 str이 "안녕하세요?"라는 값을 가지고 있는 새로운 메모리영역을 갖게 되고 처음 선언했던 "안녕"값이 할당되어 있던 메모리영역은 Garbage로 남아있다가 GC(garbage collection)에 의해 사라지게 되는 것임
* 즉, String 클래스는 불변하기 때문에 문자열을 수정하는 시점에 새로운 String 인스턴스가 생성된 것임

<br>

* String의 불변성은 변하지 않는 문자열을 자주 읽어들이는 경우에 사용하면 좋은 성능을 기대할 수 있음
* 문자열 추가, 수정, 삭제 등의 연산이 빈번하게 발생하는 알고리즘에 String 클래스를 사용하면 힙 메모리(Heap)에 많은 임시 가비지(Garbage)가 생성되어 힙메모리가 부족으로 어플리케이션 성능저하 영향을 끼침

<br>
<br>

## StringBuffer / StringBuilder
* Java에서 가변(mutable)성을 가지는 StringBuffer / StringBuilder 클래스
* String 과는 반대로 StringBuffer/StringBuilder 는 가변성 가지기 때문에 .append() .delete() 등의 API를 이용하여 동일 객체내에서 문자열을 변경하는 것이 가능함
* 문자열의 추가, 수정, 삭제가 빈번한 경우 사용하기 적합함

<br>
<br>

### StringBuffer vs StringBuilder 차이점?
* 동기화의 유무
    * StringBuffer는 동기화 키워드를 지원하여 멀티쓰레드 환경에서 안전성(thread-safe)을 가짐
        * 참고로, String도 불변성을 가지기 때문에 마찬가지로 멀티쓰레드 환경에서의 안정성(thread-safe)을 가짐
    * StringBuilder는 동기화를 지원하지 않기때문에 멀티쓰레드 환경에서 사용하는 것은 적합하지 않지만 동기화를 고려하지 않는 만큼 단일쓰레드에서의 성능은 StringBuffer 보다 뛰어남


<br>
<br>

### 정리
String: 문자열 연산이 적고 멀티쓰레드 환경일 경우  
StringBuffer: 문자열 연산이 많고 멀티쓰레드 환경일 경우  
StringBuilder: 문자열 연산이 많고 단일쓰레드이거나 동기화를 고려하지 않아도 되는 경우  

<br>

||String|StringBuffer|StringBuilder|
|:---:|:---:|:---:|:---:|
|Storage|String pool|Heap|Heap|
|Modifiable|No(immutable)|Yes(mutable)|Yes(mutable)|
|Thread safe|Yes|Yes|No|
|Synchronized|Yes|Yes|No|
|Performance|Fast|Slow|Fast|



<br>
<br>


## Ref
https://ifuwanna.tistory.com/221
