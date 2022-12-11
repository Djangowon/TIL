# JVM은 무엇이며 자바 코드는 어떻게 실행하는가?

<br>
<br>

>   JVM이란 무엇인가
# Java Virtual Machine
* 자바 가상 기계
* 자바로 작성된 애플리케이션은 모두 JVM에서만 실행됨
> 일반 애플리케이션 > OS > 하드웨어
> 자바 애플리케이션 > JVM > OS > 하드웨어

* 장점
	* 자바 애플리케이션은 OS와 하드웨어에 독립적이라 다른 OS에서도 프로그램의 변경없이 실행 가능, JVM이 OS에 종속적이기 때문에 OS에서 실행가능한 JVM 필요 ex) 윈도우용 JVM, 리눅스용 JVM, 매킨토시용 JVM 등

<br>
<br>


>  컴파일 하는 방법
## Compile
	* cmd/[자바 파일 있는 경로]/javac 파일명.java
  
<br>
<br>

>  실행하는 방법
## Run
	* cmd/[class 파일 있는 경로]/java 파일명
  
<br>
<br>

>  바이트코드란 무엇인가
# Java bytecode
* 확장자 .class
* 자바 가상 머신이 이해할 수 있는 언어로 변환된 자바 소스 코드
* 자바 컴파일러에 의해서 변환되는 코드의 명령어 크기가 1바이트라서 자바 바이트 코드라고 부름
* JVM만 있으면 어떤 OS에서도 실행 가능함

<br>
<br>

>  JIT 컴파일러란 무엇이며 어떻게 동작하는지
# Just In Time 
* JVM에서 바이트 코드들을 기계어로 번역하는 컴파일러
* Java는 프로그램 실행 시점 전인 컴파일 타임에 바이트 코드로 변환되는데, JVM에서 바이트 코드를 실행시키려면 바이트 코드를 기계어로 변환하는 단계가 필요함
> .java (java source) > Compiler > .class (bytecode) > JIT compiler > native code

* JIT 컴파일러는 컴파일 방식과 인터프리터 방식 두가지를 혼합한 방식으로 생각할 수 있음
* 실행 시점에서 인터프리터 방식으로 기계어 코드를 생성하면서 그 코드를 캐싱해서 같은 함수가 여러 번 불릴 때 매번 기계어 코드 생성하는 것을 방지함
	-   JIT 컴파일러는 바이트코드를 native code로 바꾸기 때문에 실행이 빠르지만 nativecode로 변환하는데 비용이 발생함
	-   이런 변환 비용 때문에 jvm은 모든 코드를 JIT Compiler방식으로 실행하지 않고 인터프리터 방식을 사용하다 자주 사용되는 코드만 캐싱함
	-   JVM은 내부적으로 어떤 메서드가 얼마나 자주 수행되는지를 확인하고 HotSpot(성능 저하가 될만한 부분)이라고 판단하면 컴파일을 수행해놓음
	- C1 : 런타임에 바이트코드를 기계어로 변환, C2 : 기계어로 변환해서 캐싱하는 과정
  
<br>
<br>

>  JVM 구성 
# Java Virtual Machine의 구성요소
* 클래스 로더(class loader) : 한 번에 메모리에 모든 클래스를 로드하는 것이 아닌, 필요한 순간에 해당 클래스(.class) 파일을 찾아 메모리에 로딩해주는 역할
	* 로딩
	* 링킹
		* Verify : .class 파일 형식이 유효한지 확인
		* Prepare : 클래스의 static 변수와 기본값에 필요한 메모리 공간 준비
		* Resolution : 심볼릭 메모리 레퍼런스를 실제 레퍼런스로 교체(ex. a 라는 참조변수가 힙에 저장된 실제 A 클래스를 가리킬 수 있도록 연결)
	* 초기화 : static으로 선언된 변수와 메소드에 메모리를 할당, 초기값을 채우는 과정
* JVM 실행 엔진(Execution Engine)
	* 자바 인터프리터(interpreter) : 자바 컴파일러에 의해 변환된 바이트 코드를 읽고 한 줄씩 기계어로 해석하는 역할
	* JIT 컴파일러(Just-In-Time compiler)
	* 가비지 컬렉터(garbage collector) : 자동 메모리 관리, 힙 영역에서 메모리가 사용 안 될 때
* 런타임 데이터 영역(Runtime Data Area) : 프로그램을 수행하기 위해 OS에서 할당받은 메모리 공간
## 자바 프로그램 실행과정

	1.  프로그램이 실행되면 JVM은 OS로부터 이 프로그램이 필요로 하는 메모리를 할당받는다. JVM은 이 메모리를 용도에 따라 여러 영역으로 나누어 관리한다.
	2.  자바 컴파일러(javac)가 자바 소스코드(.java)를 읽어들여 자바 바이트코드(.class)로 변환시킨다.
	3.  Class Loader를 통해 class파일들을 JVM으로 로딩한다.
	4.  로딩된 class파일들은 Execution engine을 통해 해석된다.
	5.  해석된 바이트코드는 Runtime Data Areas 에 배치되어 실질적인 수행이 이루어지게 된다. 이러한 실행과정 속에서 JVM은 필요에 따라 Thread Synchronization과 GC같은 관리작업을 수행한다.

<br>
<br>

>  JDK와 JRE의 차이
# Java Development Kit
* 자바 개발도구
* JDK 설치할 때 JVM, 자바 클래스 라이브러리, javac, javadoc 등의 개발도구, 실행에 필요한 JRE가 포함됨
* 버전 11이상 권장
## JDK/bin
	* javac.exe : 자바 컴파일러, 자바소스코드 -> 바이트코드로 컴파일
	* java.exe : 자바 인터프리터, 컴파일러가 생성한 바이트코드 해석&실행
	* javap.exe : 역어셈블러, 컴파일된 클래스파일을 원래 소스로 변환

# Java Rumtime Environment
* 자바로 작성된 응용프로그램이 실행되기 위한 최소환경
* 프로그램 실행에 필요한 라이브러리와 API, JVM이 포함됨
* 개발(쓰기)는 안되고 실행(읽기)만 가능함
