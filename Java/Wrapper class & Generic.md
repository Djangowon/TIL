# Wrapper class & Generic

<br>
<br>

## Wrapper class
* 기본 타입에 해당하는 데이터를 객체로 포장해 주는 클래스를 래퍼 클래스(Wrapper class)라고 함

|기본 type|Wrapper class|
|:---:|:---:|
|byte|Byte|
|short|Short|
|int|Integer|
|long|Long|
|float|Float|
|double|Double|
|char|Character|
|boolean|Boolean|

<br>
<br>

## Boxing & UnBoxing
* 기본 타입의 데이터를 래퍼 클래스의 인스턴스로 변환하는 과정을 박싱(Boxing)
* 래퍼 클래스의 인스턴스에 저장된 값을 다시 기본 타입의 데이터로 꺼내는 과정을 언박싱(UnBoxing)
* 래퍼 클래스(Wrapper class)는 산술 연산을 위해 정의된 클래스가 아니므로, 인스턴스에 저장된 값을 변경할 수 없음
* 즉, 값을 참조하기 위해 새로운 인스턴스를 생성하고, 생성된 인스턴스의 값만을 참조할 수 있음

<br>
<br>


## AutoBoxing & AutoUnBoxing
* 박싱과 언박싱을 자바 컴파일러가 자동으로 처리해주도록 자동화된 것이 오토박싱과 오토언박싱
* 오토박싱을 이용하면 new 키워드를 사용하지 않고 자동으로 인스턴스를 만들 수 있음
* 언박싱을 위한 intValue(), charValue() 같은 메소드를 사용하지 않아도 오토언박싱을 이용하여 인스턴스에 저장된 값을 바로 참조할 수 있음

```java
Integer num = new Integer(7); // 박싱
int n = num.intValue();        // 언박싱

Character ch = 'X'; // Character ch = new Character('X'); : 오토박싱
char c = ch;        // char c = ch.charValue();           : 오토언박싱
```

<br>
<br>

* 래퍼 클래스의 비교 연산도 오토언박싱을 통해 가능해짐
* 인스턴스에 저장된 값의 동등 여부를 정확히 판단하려면 equals() 메소드를 사용해야 함
    > 래퍼 클래스도 객체이므로 동등 연산자(==)를 사용하게 되면, 두 인스턴스의 값을 비교하는 것이 아니라 두 인스턴스의 주소값을 비교하기 때문에


<br>
<br>


## Generic
* 제네릭은 클래스나 메소드에서 사용할 내부 데이터 타입을 컴파일 시에 미리 지정하는 방법
* JDK 1.5 이전에서는 여러 타입을 사용하는 대부분의 클래스나 메소드에서 인수나 반환값으로 Object 타입을 사용했는데, Object 객체를 다시 원하는 타입으로 변환해야 하기때문에 제네릭이 도입됨
* 컴파일 시에 미리 타입이 정해지고 타입 체크를 하기 때문에, 타입 변환(형변환)을 하지 않아도 되고 버그를 줄일 수 있음

<br>
<br>

## 제네릭의 선언 및 생성
```java
class MyArray<T> {
    T element;
    void setElement(T element) { this.element = element; }
    T getElement() { return element; }
}
```
* < T > 는 타입 변수(type variable)라고 하며, 임의의 참조형 타입임
    > 타입 T는 컴파일 시에 실제 타입으로 변경됨
* 여러 개의 타입 변수를 주고 싶으면 쉼표(,)로 구분하여 지정해줄 수 있음
* 타입 변수는 클래스에서뿐만 아니라 메소드의 매개변수나 반환값으로도 사용할 수 있음

```java
MyArray<Integer> myArr = new MyArray<Integer>();
```
* 타입 변수 자리에는 기본 타입을 바로 사용할 수 없고, wrapper class로 감싸서 사용해야 함
    > 타입 변수 자리에는 객체를 넣어줘야 하기 때문에

```java
MyArray<Integer> myArr = new MyArray<>(); // Java SE 7부터 가능
```
* Java SE 7부터 인스턴스 생성 시 타입을 추정할 수 있는 경우에는 타입을 생략할 수 있음


<br>
<br>


## 제네릭의 제거 시기
* 자바 코드에서 선언되고 사용된 제네릭 타입은 컴파일 시 컴파일러에 의해 자동으로 검사되어 타입 변환됨
* 이 후에, 코드 내의 모든 제네릭 타입은 제거되어 컴파일된 class 파일에는 어떠한 제네릭 타입도 포함되지 않게 됨
* 이런 식으로 동작하는 이유는 제네릭을 사용하지 않는 코드와의 호환성을 유지하기 위해서.


<br>
<br>

## 타입 변수 제한
* 제네릭은 'T'와 같은 타입 변수(type variable)를 사용하여 타입을 제한하는데, 이때 extends 키워드를 사용하면 타입 변수에 특정 타입만을 사용하도록 제한할 수 있음
* 클래스의 타입 변수에 제한을 걸어 놓으면 클래스 내부에서 사용된 모든 타입 변수에 제한이 걸림
* 이때에는 클래스가 아닌 인터페이스를 구현할 경우에도 implements 키워드가 아닌 extends 키워드만 사용해야 함
* 클래스와 인터페이스를 동시에 상속받고 구현해야 한다면 엠퍼센트(&) 기호 사용



<br>
<br>

## generic method
* 제네릭 메소드란 메소드의 선언부에 타입 변수를 사용한 메소드를 의미함
```java
public static <T> void sort( ... ) { ... }
```

* 제네릭 클래스에서 정의된 타입 변수 T와 제네릭 메소드에서 사용된 타입 변수 T는 별개임


<br>
<br>

## wild card
* 와일드카드(wild card)란 이름에 제한을 두지 않음을 표현하는 데 사용되는 기호를 의미함
* 자바의 제네릭에서는 물음표(?) 기호를 사용하여 이러한 와일드카드를 사용할 수 있음
```
<?>           // 타입 변수에 모든 타입을 사용할 수 있음.
<? extends T> // T 타입과 T 타입을 상속받는 자손 클래스 타입만을 사용할 수 있음.
<? super T>   // T 타입과 T 타입이 상속받은 조상 클래스 타입만을 사용할 수 있음.
```



<br>
<br>

## Ref
http://www.tcpschool.com/java/java_api_wrapper  
http://www.tcpschool.com/java/java_generic_concept  
http://www.tcpschool.com/java/java_generic_various  
https://codechacha.com/ko/java-generics/  
https://gangnam-americano.tistory.com/47  

