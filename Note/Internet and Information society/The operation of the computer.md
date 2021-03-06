# The operation of the computer
## 소프트웨어의 이해
* 소프트웨어: 다양한 장치들을 동작시켜 특정 작업을 해결하는 프로그램
* 하드웨어: 컴퓨터는 구성하고 있는 물리적 부품

### 소프트웨어의 종류
* 응용 소프트웨어
    * 사용자의 업무나 목적에 맞게 개발된 프로그램
    * 문제 해결 방법을 프로그램의 형태로 만들고 사용자가 필요에 따라 선택하여 사용하는 프로그램

* 시스템 소프트웨어
    * 하드웨어를 제어·관리할 수 있도록 설계된 소프트웨어
    * 응용 소프트웨어를 실행하기 위한 환경을 제공

### 시스템 소프트웨어의 이해
* 다양한 장치들을 서로 유기적으로 동작시켜 특정 작업을 수행할 수 있는 환경을 조성하는 프로그램
* 시스템 소프트웨어의 종류
    * 운영체제(커널)
        * 사용자가 컴퓨터를 효율적으로 운영·관리·사용할 수 있도록 하드웨어를 제어하는 소프트웨어
    
    * 컴파일러
        * 소스코드를 컴퓨터가 이해할 수 있는 기계어로 번역하는 소프트웨어
   
   * 유틸리티
        * 추가적인 기능을 제공하여 사용자가 컴퓨터를 효율적이고 편리하게 관리할 수 있도록 지원해주는 소프트웨어

## 운영체제의 이해
### 운영체제의 역할
* 응용 소프트웨어가 효과적으로 작동할 수 있는 환경을 조성
    > 처리능력, 사용 가능도, 응답시간, 신뢰성

### 운영체제의 기능
* 컴퓨터의 자원(장치)을 효율적으로 관리하고 프로그램에 자원을 할당
* 컴퓨터 시스템의 기능을 사용할 수 있도록 지원
    * 사용자 인터페이스
        * 컴퓨터와 사용자를 연결해주는 매개체
        * 컴퓨터와 사용자가 상호작용하는 방법을 의미
        * CLI(Command Line Interface) / GUI(Graphic User Interface)
    
    * 프로세스 관리
        * 프로세스는 실행되고 있는 상태의 프로그램
        * 여러 프로그램 실행이 요청되면 한정된 자원(기억장치 등)을 효과적으로 사용하도록 조율
    
    * 네트워크 관리
        * 컴퓨터는 네트워크를 통해 상호 데이터 교환
        * 통신 프로그램(소프트웨어) 제공 및 통신 장치(하드웨어) 관리
    
    * 기억·저장장치 관리
        * 보조기억장치(하드디스크 등)에 저장된 컴퓨터의 프로그램은 실행되기 위해서 주기억장치(메인메모리)에 적재
        * 보조기억장치의 크기가 주기억장치보다 매우 크기 때문에 주기억장치의 효율적 관리가 요구
    
    * 입출력장치 관리
        * 입력장치를 통해 사용자로부터 입력받고 출력장치를 사용하여 처리 결과(데이터)를 출력

## 운영체제의 종류
* 사용자들의 작업 목적에 따라 여러 종류의 운영체제가 개발
    * 데스크탑 또는 서버환경
        > DOS, OS2, 윈도우, Mac OS, 유닉스 계열, 리눅스 계열, 크롬 OS

    * 모바일 환경
        > iOS, 안드로이드, 심비안, 블랙베리, 타이젠, 우분투 터치 등

#### DOS(Disk Operating System)
* 대표적인 텍스트 기반의 CLI 운영체제
    * 단일 태스크만 지원
    * MS-DOS, DR-DOS, PC-DOS 등 여러 종류가 있으나 우리나라의 경우 MS-DOS를 많이 사용

#### OS/2, OS/2 WARP
* 마이크로소프트사와 IBM의 공동 제작한 OS
    * DOS의 한계를 극복한 멀티 태스크 OS
    * GUI 방식의 인터페이스 및 폴더 개념 도입

#### Windows
* 마이크로소프트에서 제작한 OS
    * 윈도우 3.0, 윈도우 95, 윈도우XP, 윈도우 7, 윈도우 11 등 전세계 가장 많이 사용되는 OS
    * USB 및 플러그 앤 플레이(PnP) 기능 최초 지원

#### UNIX
* AT&T 벨 연구소의 중형컴퓨터를 위해 개발된 OS
    * 다수의 사용자가 이용할 수 있는 멀티유저 OS
    * 고급언어(C)로 개발된 최초의 OS

#### Linux
* 리처드 스톨만의 GNU(Gnu is Not Unix) 프로젝트의 일환으로 개발된 OS
    * 1991년 리누스 토발즈에 의해 개발된 OS
    * 200여 종류가 넘는 배포판이 존재

#### Mac OS
* 애플 매킨토시 용으로 개발된 OS
    * 유닉스 OS가 기반
    * 최초 GUI 방식을 도입한 개인용 컴퓨터 OS
    * 모바일 OS인 iOS, ipadOS의 모체

### 모바일 OS의 개념
* 스마트폰, 태블릿, PDA 등의 모바일 장치를 제어하는 운영 체제
* 애플의 iOS와 안드로이드 OS가 시장을 양분

#### iOS
* 애플 사의 아이폰, 아이팟 터치, 아이패드 등의 기기에 설치되는 유닉스 기반의 모바일 OS
    * 앱스토어를 통해 사용자앱을 배포하여 자체적인 모바일 생태계 최초로 구성

#### 안드로이드 OS
* 구글 사에서 개발한 리눅스 기반의 개방형 OS
    * 정확히는 리눅스 기반의 커널 사용 
    * 자바(코틀린) 기반의 앱 개발 환경 제공
    * 전세계 60% 이상의 스마트 폰에 설치

#### 기타 모바일 OS
* 심비안 - 심비안에서 개발한 모바일 OS
* 블랙베리 - 블랙베리 스마트폰 용 OS, 이메일과 일정 관리 등 비즈니스 부분에서 강점
* 타이젠 - 삼성전자, 인텔, 리눅스 재단 등과 협력해, 애플과 구글에 대항할 새로운 리눅스 기반의 모바일 OS
* 우분투 터치 - 리눅스 기반의 모바일 OS로 리눅스 기반의 사용자 앱 사용 가능
