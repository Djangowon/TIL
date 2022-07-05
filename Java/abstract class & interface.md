# abstract class & interface


<br>

## abstract method
* 추상 메소드(abstract method)란 자식 클래스에서 반드시 오버라이딩해야만 사용할 수 있는 메소드를 의미함
* 자바에서 추상 메소드를 선언하여 사용하는 목적은 추상 메소드가 포함된 클래스를 상속받는 자식 클래스가 반드시 추상 메소드를 구현하도록 하기 위함
* 즉, 추상 메소드는 선언부만 존재하고, 구현부를 작성을 자식 클래스에서 오버라이딩해서 사용해야 함

```java
abstract 반환타입 메소드이름();  // 세미콜론; -> 구현부가 없단 의미
```

<br>
<br>

## abstract class
* 추상 클래스(abstract class)란 하나 이상의 추상 메소드를 포함하는 클래스
* 추상 메소드뿐만 아니라 생성자, 필드, 일반 메소드도 포함할 수 있음
* 추상 클래스는 동작이 정의되어 있지 않은 추상 메소드를 포함하고 있기 때문에 인스턴스를 생성할 수 없음
* 추상 메소드가 포함된 추상 클래스를 상속받은 모든 자식 클래스는 추상 메소드를 구현해야만 인스턴스를 생성할 수 있으므로, 반드시 구현하게 됨
    
### example code
```java
abstract class Device {
    abstract void pay();
}

class Apple extends Device {
    void pay() {
        System.out.println("애플페이");
    }
}

class Samsung extends Device {
    void pay() {
        System.out.println("삼성페이");
    }
}

public class Abstract {
    public static void main(String[] args) {
//        device a = new Device();  -> 추상 클래스이기 때문에 인스턴스 생성할 수 없음

        Apple apple = new Apple();
        Samsung samsung = new Samsung();

        apple.pay();
        samsung.pay();
    }
}
```

<br>
<br>

# interface
* 클래스는 다중 상속을 받을 수 없지만, 인터페이스는 통한 다중 상속을 받을 수 있음
* 추상 메소드, 상수만을 포함할 수 있음
* 인터페이스의 모든 필드는 public static final이어야 하며, 모든 메소드는 public abstract이어야 함

```java
접근제어자 interface 인터페이스이름 {

    public static final 타입 상수이름 = 값;

    ...

    public abstract 메소드이름(매개변수목록);

    ...

}
```

<br>
<br>

### example code
```java
interface Device {public abstract void pay();}
interface Phone {public abstract void call();}

class Apple implements Device {
    @Override
    public void pay() {
        System.out.println("애플페이임");
    }
}

class Samsung implements Device {
    @Override
    public void pay() {
        System.out.println("삼성페이임");
    }
}

class IPad extends Apple implements Device {   // 상속과 구현 동시에 가능함
    @Override
    public void pay() {
        System.out.println("애플페이만 사용가능");
    }

}

class IPhone implements Device, Phone {   // 인터페이스 다중 상속

    @Override
    public void pay() {
        System.out.println("애플페이 결제하기");
    }

    @Override
    public void call() {
        System.out.println("전화걸기");
    }
}

public class Interface {
    public static void main(String[] args) {
        Apple apple = new Apple();
        Samsung samsung = new Samsung();
        IPad iPad = new IPad();
        IPhone iPhone = new IPhone();

        apple.pay();
        samsung.pay();
        iPad.pay();
        iPhone.pay();
        iPhone.call();
    }
}

```
### 인터페이스의 장점
1. 대규모 프로젝트 개발 시 일관되고 정형화된 개발을 위한 표준화가 가능함
2. 클래스의 작성과 인터페이스의 구현을 동시에 진행할 수 있으므로, 개발 시간을 단축할 수 있음
3. 클래스와 클래스 간의 관계를 인터페이스로 연결하면, 클래스마다 독립적인 프로그래밍이 가능함


<br>
<br>

## Ref
http://www.tcpschool.com/java/java_polymorphism_abstract  
http://www.tcpschool.com/java/java_polymorphism_interface  
