# Selection Control Statement and Repetition Statement
## 선택 제어문과 반복 제어문
* 프로그램 언어의 제어 구조
    * 순차적 제어
        * 특별한 지정이 없는 한 위에서 아래로 수행되는 제어구조

    * 선택적 제어
        * 주어진 조건에 따라 `특정부분으로 수행을 옮기는` 분기 제어구조

    * 반복적 제어
        * 특정 부분을 일정한 `횟수만큼 반복 수행하는` 반복 제어구조

## 선택 제어문
* if문
* switch ~ case문
* goto문

### if문
* 형식:
```C
if(조건)
    명령문 1;
    명령문 2;
```

* 단순 if문의 사용 예시

```C
#include <stdio.h>
void main() {
    int a=10, b=20;
    if(a>b) { #조건을 만족하지 않으므로 중괄호 밖의 명령문을 수행
        a=a+20;
        printf("a=%d\n",a);
    }
    b=b+20; #여기
    printf("b=%d",b);
}
```

### if ~ else문
* 형식:
```C
if(조건)
    명령문 1;
else
    명령문 2;
```
* 기능: 주어진 조건이 참일 때는 명령문 1을, 거짓일 때는 명령문 2를 수행함

### 다중 if ~ else문
* 형식: 
```C
if(조건 1)
    if(조건 2)
        명령문 1;
    else
        명령문 2;
else
    명령문 3;
```
* 기능: 조건 1과 조건 2가 참일 때 명령문 1을, 조건 1이 참이고 조건 2가 거짓일 때는 명령문 2를, 조건 1이 거짓일 경우는 명령문 3을 수행함

### 다중 if ~ else if ~ else 문
* 형식:
```C
if(조건 1)
    명령문 1;
else if(조건 2)
    명령문 2;
else if(조건 3)
    명령문 3;
else
    명령문 4;
```
* 기능: 조건 1이 참이면 명령문 1을 수행하고, 거짓이면 조건 2를 검사하여 참이면 명령문 2를 수행하고, 거짓이면 조건 3을 검사하여 참이면 명령문 3을 수행하고, 거짓이면 명령문 4를 수행함

### switch ~ case 문
* 형식:
```C
switch(수식)
{
    case 값1: 명령문 1;
    case 값2: 명령문 2;
        ...
    default: 명령문 n;
}
```
* 기능: 주어진 값에 따라 여러 곳 중 한 곳으로 분기하여 실행

* switch ~ case 문의 사용 예시

```C
#include <stdio.h>
#pragma warning(disable:4996)
void main() {
    int n;
    printf("n=?");
    scanf("%d",&n);
    printf("\n n % % 5 = %d\n",n%5);
    switch(n%5) { #입력된 수를 5로 나누어 그 나머지에 해당되는 경우로 분기
        case 0: printf("나머지는 0\n");
        break;
        case 1: printf("나머지는 1\n");
        break;
        case 2: printf("나머지는 2\n");
        break;
        default: printf("나머지는 3이나 4\n");
        break;
    }   
}
```

### goto 문(무조건 분기)
* 형식: 
```C
Label:

goto Label;
```
* 기능: 프로그램 수행 도중에 원하는 곳으로 제어를 무조건적으로 옮김

* goto 문의 사용 예시
```C
#include <stdio.h>
#pragma warning(disable:4996)
void main() {
    int i, n, c='A';
    while(1) {
        printf("\n 횟수는 ?");
        scanf("%d", &n);
        for(i=1; i<=n; i++) { #n회 반복하는 for 반복문
            printf("%c", c);
            if(c=='Q')
                goto end; #레이블 명 end로 무조건 실행을 옮김
            c++;
        }
    }
    end: #레이블 명(레이블 명 다음에는 콜론(:)을 붙임)
    printf("\n\n 끝");
}
```
* goto 문의 사용될 수 없는 경우
    * 레이블의 위치가 어느 특정 루프 안에 들어있는 경우는 사용 불가

## 반복 제어문
* 반복 제어문의 종류
    * for문
    * while문
    * do ~ while문

### for문
* 형식:
```C
for(초기식; 조건식; 증감식) {
    반복 실행될 문장
}
```
* 기능: 주어진 조건이 만족되는 동안 루프문을 반복 수행함

* for문의 사용 예시
```C
#include <stdio.h>
void main() {
    int i, sum=0; #루프변수 i는 정수형이어야 함
    for (i=0; i<=10; ++i) #for 반복문(루프문)
        sum=sum+i; #i값이 11이 되면 조건식이 거짓이 되어 루프를 빠져나옴
    printf("1부터 %d까지의 합=%d", i-1, sum);
}
```

### 다중 for문
* 형식:
```C
for(초기식; 조건식; 증감식) {
    for(초기식; 조건식; 증감식) {
        for(초기식; 조건식; 증감식) {
            반복 실행될 문장
        }
    }
}
```
* 기능: 주어진 조건이 만족되는 동안 루프문을 반복 수행함

### while문
* 형식:
```C
while(조건식) {
    반복 실행될 문장;
}
```
* 기능: 주어진 조건이 만족되는 동안 루프문을 반복 수행함

* while문의 사용 예시
```C
#include <stdio.h>
void main() {
    int i=0;
    int sum=0;
    while(i<=100){
        sum=sum+i;
        i++;
    }
    printf("1부터 100까지의 합=%d", sum);
}
```

### do ~ while문
* 형식:
```C
do {
    반복 실행될 문장;
}while(조건식);
```
* 기능: 반복문 내의 명령문을 실행한 후, 주어진 조건을 검사하여 반복 수행 여부를 결정함

* do ~ while문의 사용 예시
```C
#include <stdio.h>
void main() {
    int i=0; n;
    int sum=0;
    printf("n=?");
    scanf("%d",&n);
    do { #do ~ while 루프
        sum=sum+i;
        i++;
    }while(i<=n); #세미콜론(;)을 쓰지 않으면 에러 발생
    printf("i=%d\n",i);
    printf("i ~ %d까지 합=%d\n",n,sum);
}
```

## 기타 제어문
* 기타 제어문의 종류
    * break문
        * break문은 반복 명령의 실행 도중에 강제적으로 반복문을 빠져 나오는 데 사용
            * for 루프, while 루프, do ~ while 루프, switch 블록 등을 강제로 종료시키고자 할 때 사용
        * break문은 자신이 포함된 반복문만 빠져 나옴

    * continue문
        * continue문은 루프 실행 중에 루프를 다시 실행하고자 할 때 사용
            * switch ~ case 문에서는 사용하지 않고, 반복구조에만 국한되어 사용
        * continue 문은 그 루프의 선두로 제어를 옮겨 다음 반복을 실행

