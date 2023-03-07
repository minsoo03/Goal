Pointer Note
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
