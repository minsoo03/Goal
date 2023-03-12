C Note
=============

데이터 주소값 : 해당 데이터가 저장된 메모리의 시작 주소 

특히 C언어 -> 1 바이트 크기의 주소값들을 메모리 공간으로 나누어 표현

( ex. int형 데이터는 4바이트! but, 주소 값은 시작 주소 오직 1 바이트만 )



![1](https://user-images.githubusercontent.com/54320003/223411324-264a930d-b03a-4337-aa58-062004c1a2c2.png)


### What is Pointer?

C언어에서 포인터란? => 메모리 주소값 저장 변수 ( = 포인터 변수 )

이건 마치 int형 변수는 정수를 , char형 변수는 문자를 저장하는 것처럼 포인터 변수는 "주소값" 저장

ex.
<pre>
<code>
int n = 100; // 이건 변수 선언
int *ptr = &n; // 이건 포인터 선언 
</code>
</pre>



![2](https://user-images.githubusercontent.com/54320003/223412846-ab059550-98a5-41b0-902e-a29d48f2ac8d.png)

= 사용된 변수와 포인터가 메모리에서 어떻게 저장되는 지 보여주는 예제



ex.
<pre>
<code>
#include <stdio.h>

int main()
{
    char s1[50], s2[50] = "Hello";
    
    s1 = s2;
    printf("%s", s1);

    return 0;
}
</code>
</pre>

## 이 코드가 컴파일 에러가 나는 이유 

->  문자열 배열은 저장하기 위한 메모리 공간을 할당한다. 
s1과 s2는 모두 문자열 배열이며 포인터 간에 대입이 되지 않는다. 문자열을 복사하려면 "strcpy()" 함수를 사용해야 한다. strcpy(s1, s2);를 사용 해야한다..!


ex.
<pre>
<code>
#include <stdio.h>

int main()
{
    int *ptr, x;

    ptr = &x;
    *ptr = 0;

    printf(" x = %dn", x);
    printf(" *ptr = %dn", *ptr );

    *ptr += 5;
    printf(" x = %dn", x);
    printf(" *ptr = %dn", *ptr);

    (*ptr)++;
    printf("x = %dn", x);
    printf(" *ptr = %dn", *ptr);

    return 0;
</code>
</pre>

=> ptr 와 x는 int형의 포인터 변수
ptr은 x의 메모리 주소로 설정

*ptr = 0으로 포인터를 통해 x의 값 0 
그리고 *ptr에 5를 더하고 *ptr++으로 포인터 값 1 증가 시킴

* 출력값 -> x = 0 , *ptr = 0, *ptr =5, x =6, *ptr = 6

x와 *ptr의 값은 모두 변경된당. ptr이 x의 메모리 주소이기 때문!! 그러므로 *ptr을 통해 x의 값을 직접 변경 할 수 있다. 쉽노 ㅋ


ex.
<pre>
<code>
#include <stdio.h>

int main()
{
    int arr[] = {10 , 20, 30, 40, 50, 60};
    int *ptr1 = arr;
    int *ptr2 = arr + 5;

    printf("number of elements between two pointers : %d\n", (ptr2 - ptr1));
    printf("number of bytes between two pointers : %d\n", (char*)ptr2 - (char*)ptr1);
    return 0;
}
</code>
</pre>

-> 
1. main 함수에서 int 형 배열 arr 선언, 몇 개의 정수값 초기화

**잠깐!! -> 여기서 초기화 하는 이유는 c에선 배열이 스택에 잡힌다. 스택에 잡히는 변수는 실행 전 컴파일 시점에서 알아야 해서, 실행 중 입력 받아 크기를 잡을 수 없다. 따라서 배열의 크기는 상수로 선언 해야함.

2. 두 개의 포인터 변수 ptr1 , ptr2 선언 / arr 의 첫번째 요소 & 마지막 요소에 대한 포인터 가리킴
3. ptr1와 ptr2 사이의 요소 수와 바이트 계산 
4. 첫 번째 코드는, print문이 두 포인터 간의 거리를 나타내며, 포인터 간의 뺄셈으로 계산
5. 두번째 print문은 두 포인터 간의 바이트 수 계산, ptr1 와 ptr2 간의 거리를 바이트 단위로 계산
 ** 이 때, 각 포인터 타입은 int*이므로 char *를 사용하여 char 포인터로 변환!!!!! 신기하노 ㅋ
 
 
 -----
 
 #include<stdio.h> 이란 무엇인가??
 = #include는 헤더 파일을 포함하는 문법 , prinf 함수를 이용하려면 stdio.h 파일이 필요하다.
 => 다양한 함수를 사용하려면 다양한 헤더파일이 필요하다.
 
 ----
 
 C언어 프로그램은 main 함수부터 실행된다! (중요)
 
 ----
 
 ##서식 지정자
 
 서식 지정자는 printf로 문자열을 출력할 때 값으로 바뀌는 부분을 뜻한다.
 
<pre>
<code>
printf( "%s\n", "Hello World!");
</pre>
</code>
이 경우, printf에 %s를 사용한 뒤, Hello World를 넣어주면 %s 부분이 Hello world로 바뀐다. (%s는 문장 , %c는 한 단어)

----

##변수

정수 : char , short, int, long
실수 : float, double
포인터 사용할 시 : void

"변수를 초기화한다" = 변수를 선언하면서 값을 할당하는 과정



----

#정수 자료형

signed : 부호 있는 정수 , 보통 signed 는 생략한다.
unsigned : 부호 없는 정수 표현 , 값은 0부터 시작한다.

|자료형|크기|범위|
|------|---|---|
|char , signed char|1byte , 8bit|-128 ~ 127|
|unsigned char|1byte , 8bit|0 ~ 255|
|short|2byte , 16bit|-32,768 ~ 32,767|
|unsigned short|2byte , 16bit|0 ~ 65,535|
|int, signed|4byte , 32bit| ~ |
|unsigend|4byte , 32 bit| ~ |
|long, signed long|4byte, 32bit| ~ |
|unsigned long|4byte , 32bit| ~ |
|long long, signed long long|8byte, 64bit| ~ |
|unsigned long long|8byte, 64bit| ~ |

*int는 생략 가능하다.

- 크기로 따졌을 때 (범위제외)
char < short < int , signed < long < long long

값에 대해 저장할 수 있는 최댓값을 초과하거나, 최솟값 미만 값의 type을 쓴다고 하면 오버플로우 , 언더플로우가 생긴다. -> 최솟값, 최댓값에서부터 다시 시작한다.

##자료형 크기

sizeof(자료형) 
sizeof(표현식)
sizeof 표현식
* 단, 자료형의 크기를 직접적으로 구할려면 띄어쓰기 대신 괄호

sizeof 표현식 을 통해 자료형의 크기를 구할 수 있다.

-- 실수 자료형

float - 4byte , 32bit
double - 8byte , 64bit
long double - 8byte , 64bit

-- 상수 사용하기

10진수 -> 숫자 그대로 표현
8진수 -> 숫자 앞에 0 붙이기 ( 서식 지정자는 %o 사용해야함 )
16진수 -> 0x 붙이기

상수 선언 -> 자료형 앞에 const 붙이기 
but, 상수는 반드시 선언과 동시에 값 할당 -> 초기화 시켜주어야함 ( 초기화 하지 않으면 컴파일 에러)

