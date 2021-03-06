---
layout: post
title: "[프로그래밍 언어론] 데이터 타입(1)"
author: "Soy-A"
comments: true
tags:
- Programming Language
---

- 데이터 타입(data type): 데이터 값들의 모임과 그들 값들에 대한 미리 정의된 연산들의 집합을 정의
- **서술자**(descriptor): 변수의 속성들의 모임
  - 구현(implementation)에서, 서술자는 **변수의 속성들을 저장**하는 메모리의 영역을 의미
  - 모든 경우, 서술자는 **타입 검사**를 위해 사용되고 할당(allocation)과 회수(deallocation) 연산을 위한 코드를 생성하는데 사용됨<br/><br/>


# 기본 데이터 타입(primitive data types)

- 다른 타입들의 관점에서 정의되지 않은 데이터 타입

---

## 수치 타입(numeric types)

- 초기의 많은 프로그래밍 언어들은 수치(numeric) 기본 타입들만 제공
- 여전히 중심적인 역할

### 정수(integer)

- 가장 공통된 기본 수치 데이터 타입
- 대부분의 정수 타입은 **하드웨어**에 의해 직접 지원됨
- Java: byte, short, int, long
- C++, C#: unsigned integer
- 음의 정수 표기법
  - 부호-크기 표기법(sign-magnitude notation)
  - 1의 보수(one's complement)
  - 2의 보수(two's complement)
<br/><br/>

### 부동-소수점 수(floating point)

- 실수를 모델링하지만, 그 표현은 단지 대부분의 실수 값에 대한 **근사 값**임
> 실제로 다음과 같은 코드를 실행시켜보면, 아래와 같은 계산 결과를 볼 수 있다.<br/>
```
float a = 1.1;
float b = 2.2;
printf("%.10f", a+b);
```
=> 3.3000001907(또는 다른 숫자)
- 포맷: IEEE Floating Point Standard 754
- 대부분의 언어는 두 가지 부동-소수점 수의 타입을 포함: float, double
- 대체로 하드웨어와 같지만 항상은 아님
- 부동-소수점 수 타입으로 표현될 수 있는 값들의 집합은 정밀도(precision)와 범위(range)의 관점에서 정의됨
- 정확한 계산 위해서는 floating point 사용하지 않는다
<br/><br/>

### 복소수(complex)

- Fortran, Python과 같은 언어는 복소수를 지원한다
- 순서화된 부동-소수점 수의 값들의 쌍으로 표현된다
> 7 + 3j

<br/>
### 십진수(decimal)

- 사무 시스템 응용 분야를 지원하기 위해 설계된 대부분의 규모가 큰 컴퓨터들은 십진수(decimal) 데이터 타입을 위한 하드웨어 지원을 포함함
- 장점: 제한된 범위에 포함된 십진수 값들을 **정확**하게 저장 가능
- 단점: 범위가 제한적, **메모리 낭비**(이진수 표현보다 많은 메모리 차지)
- 십진수 타입은 십진수 숫자를 위한 이진수 코드를 사용하여 문자 스트링과 매우 흡사하게 저장됨
  - **BCD**(binary coded decimal)
  - **바이트당 두 개의 숫자**가 축약되어 저장됨
<br/><br/>

### 불리안(boolean) 타입

- 가장 단순한 타입
- 단 두 개의 요소만을 가짐(true, false)
- 한 개의 비트로 표현될 수 있다. 그러나 **효율적 접근을 위해 한 개의 바이트에 저장**된다.
- 프로그램에서 스위치나 플래그를 표현하는 데 사용됨
- **readability**를 높인다
<br/><br/>

### 문자(character) 타입

- 문자 데이터는 수치 코딩으로 컴퓨터에 저장됨
> - ASCII: 128개의 다른 문자(1byte)<br/>
>- ISO 8859-1: 256개의 다른 문자<br/>
>- 16-bit Unicode: 대부분의 자연 언어에 속한 문자들을 포함(2byte)
- 단일 문자들의 코딩 처리하는 수단 제공하기 위해, 대부분의 프로그래밍 언어는 문자들을 위한 기본 타입 포함함
<br/><br/>

### Unicode

- **전 세계의 모든 문자**를 컴퓨터에서 일관되게 표현하고 다룰 수 있도록 설계된 **산업 표준**
- 표현: U+hexadecimal
> e.g. 가 -> U+AC00
- unicode는 무조건 2byte로 표현되는 것 아님
- 기본적인 내용만 2byte에, 추가적인 것들은 나머지 2byte에 표현(총 4byte)
<br/><br/>

### UTF(Unicode Transfer Format)

- UTF-16
  - **가변길이 인코딩**
  - 아스키랑 1:1 맵핑X
  - BMP(Basic multilingual plane)- 2bytes, otherwise-4bytes로 표현
  - BMP에 속하면 2 byte로 표현하며, big endian인지 little endian인지에 따라 다르게 해석됨
  - 따라서 구분을 위해 BOM(byte order mark) 넣어줌
- UTF-32
  - **고정길이 인코딩**
  - 모든 문자 4byte로 표현
  - 직접 인덱싱되나, 공간 효율이 떨어진다
- UTF-8
  - **가변길이 인코딩**(1-4byte)
  - **ASCII와 호환**됨(U+007F까지의 문자는 7비트 아스키 문자와 동일한 방법으로 표시됨, 첫비트는 0)

<br/><br/><br/>

# 문자 스트링 타입(character string type)

- 값들이 일련의 문자들로 구성되는 타입
- 문자 스트링은 문자 조작을 하는 모든 프로그램에서 필수적인 타입임

---

## 스트링과 연산

- 배정, 접합, 부분 스트링 참조, 비교, 패턴 매칭


### C와 C++

- 스트링이 기본 타입으로 정의되지 않음
>  char *str = "apple";<br/>

  > in **python**<br/>
a = "abcd" <br/>
b = "bcde"<br/>
a>b 또는 a==b와같은 비교가 가능하다(primitive type이므로)<br/>

  > in **C**<br/>
char배열 비교는 strcmp를 이용한다
- char 배열을 이용해 문자 스트링 저장
- 표준 라이브러리를 통해 스트링 연산들의 모음 제공

### Java

- String 클래스 (char의 배열 아님)
- Objects는 한 번 생성시 불변(**immutable**)
> 같은 이름에 다른 객체를 할당하더라도 기존 객체는 그대로 남아있다
- StringBuffer/StringBuilder 클래스의 값은 변경 가능
> for문으로 계속해서 문자를 덧붙이는 작업같은 경우 이 방법이 그냥 String을 이용하는 것보다 더 빠르다(새로운 객체 생성x)<br/>

  > StringBuffer: Not synchronized<br/>

  > StringBuilder: synchronized, multy thread

<br/>

---

## 스트링 길이 선택 사항

### 정적 길이 스트링(static length string)

- 길이 고정
- FORTRAN 77, Ada, COBOL
- 길이는 정적이고, 스트링이 생성될 때 설정됨

<br/>
### 제한된 동적 길이 스트링(limited dynamic length strings)

- C, C++
- 스트링이 그 변수 정의에서 선언되고 고정된 최대 길이까지의 가변적인 길이를 갖는 것을 허용함
> char str[100] = "Hello";	// 길이가 5로 바뀐다

<br/>
### 동적 길이 스트링(dynamic length strings)

- SNOBOL4, Perl, JavaScript, ...
- 스트링이 최대 길이의 제한 없이 가변 길이를 갖는 것을 허용

<br/>

---

## 문자 스트링 타입의 구현

### 정적 문자 스트링 타입

- compile-time descriptor(서술자)
- 타입의 이름, 길이, 첫 번째 문자에 대한 주소의 필드를 가짐

<br/>
### 제한된 동적 스트링

- 고정된 최대 길이와 현재 길이를 저장하는 run-time 서술자를 요구
> C, C++은 제외
>- 스트링의 끝이 null 문자로 표시되므로 run-time 서술자를 요구하지 않음
>- 인덱스 값에 대한 범위가 검사되지 않으므로 최대 길이가 필요하지 않음

<br/>
### 동적 길이 스트링

- 단지 현재 길이만 저장될 필요 있으므로 run-time 서술자를 요구
- 할당/반환이 가장 큰 구현 문제
- 스트링은 연결 리스트에 저장될 수 있다

<br/><br/><br/>

# 사용자-정의 순서 타입

## 열거(enumeration) 타입

- 이름 상수(열거 상수)들인 모든 가능한 값들이 그 정의에서 제공되는, 즉 열거되는 타입
- 열거타입은 열거 상수의 모임을 정의하고 그룹핑하는 방법을 제공함
> in C#<br/>
**enum** days {Mon, Tue, Wed, Thu, Fri, Sat, Sun}

- C,C++의 enum: 정수랑 매핑시킴, 임의로 정수 매핑도 가능(C++은 캐스팅 필요)
- Java, Python의 enum: 정수 매핑 불가

<br/><br/><br/>

# 배열(array) 타입

- 배열: **같은 타입의 데이터가 연속된 공간에 저장된 것**
- 개개의 원소는 집단체(aggregate)에서 첫 번째 원소와의 상대적인 그 위치에 의해 식별됨

<br/>
## 배열과 색인(indexes)

- 배열의 특정 원소들은 두 개 수준의 구문 매커니즘에 의해서 참조됨
  - 집단체 이름
  - 첨자(subscript), 색인(index)이라고 알려진 동적 가능 선택자(dynamic selector)
- 선택 연산은 배열 이름과 첨자 값들의 집합으로부터 집단체의 한 원소로의 사상(mapping)으로 생각될 수 있음
  - array = 유한 사상(finite mappings)
  - array_name(index_value_list) -> element
- 배열 참조의 구문은 매우 보편적임
  - Ada, Fortran은 소괄호 사용
  - 대부분의 언어는 대괄호 사용
- 첨자들의 타입
  - FORTRAN, C, Java...: 정수만
  - Pascal, Ada: 임의의 순서 타입 사용 허용(boolean, char, enum...)

<br/>

---

## 첨자 바인딩

- 배열 변수에 대한 첨자 타입의 바인딩은 보통 정적, but 그 첨자 값 범위는 때때로 동적으로 바인딩됨
- 어떤 언어(C, Fortran)에서, 첨자 범위의 하한(lower bound)은 묵시적임

<br/>

---

## 배열 유형

- 첨자 값 범위에 대한 바인딩, 기억공간에 대한 바인딩, 그 기억공간이 어디서 할당되는가에 기반함

### 정적 배열(static array)
- 첨자 범위 바인딩과 기억공간 할당이 정적인 배열
- 장점: 효율성(동적 할당이나 회수가 요구되지 않으므로 access측면에서 효율적임)
- 메모리 측면에서는 효율성이 떨어진다
> e.g. Fortran 77, Ada의 몇몇 배열

### 고정 스택-동적 배열(fixed stack-dynamic array)
- 첨자 범위가 정적으로 바인딩되지만, 그 할당이 실행 시간 중 선언문 세련화 시간(declaration elaboration time)에 이루어지는 배열
> e.g. int a[10]; // compile time에 스택에 위치 잡음. but 값은 run-time에 할당
- 장점: 기억공간의 효율성

### 고정 힙-동적 배열(fixed heap-dynamic array)
- 첨자 범위와 기억공간의 바인딩이 기억공간이 할당된 후에 고정됨
> e.g. new int[n]; // n=10;하는 순간 힙에 10개 fixed 됨
- 장점: 유연성

### 힙-동적 배열(heap-dynamic array)
- 첨자 범위의 바인딩과 기억공간의 할당이 동적이며, 배열의 존속기간 동안에 변경할 수 있는 배열
- 힙에서 늘어났다 줄어들었다 함
> in Java: 모든 배열은 고정 힙-동적 배열<br/>
in Perl, JavaScript: 배열은 필요에 따라 늘었다 줄었다 함

<br/>

---

## 배열 연산

- 배열 단위로 연산을 수행하는 연산(배정, 접합, 비교, 슬라이스 등)
- Python
  - **+**: 배열 접합
  - **in**: 원소 멤버십
  - **is, ==**: 비교 연산
> in Python<br/>
A = [1,2,3]<br/>
A == [1,2,3] // T(값이 같은지를 비교)<br/>
A is [1,2,3] // F(같은 object인지를 비교)

<br/>

---

## 직사각형 배열과 톱니형 배열

### 직사각형(rectangular) 배열

- 모든 **행**들이 **동일 개수의 원소**들을 포함하고, 모든 **열**들이 **동일 개수의 원소**들을 포함하는 **다차원 배열**
- 직사각형 표라고 생각하면 됨

### 톱니형(jagged) 배열

- 행들의 크기가 동일할 필요가 없는 다차원 배열(**가변**)
- 행, 열 길이 각각 지정 가능

>- **C, C++, C#, Java**<br/>
  - jagged array 지원
  - 원소 참조: myArray[3][7]
- **Fortran, Ada, C#**<br/>
  - rectangular array 지원
  - 원소 참조: myArray[3, 7]

<br/>

---

## 배열 타입의 구현

- 배열 원소의 접근을 허용하는 코드는 compile-time에 생성되어야 함
- run-time에, 코드가 원소의 주소를 생성하도록 실행되어야 함

### 1차원 배열

- 인접한 메모리 셀들의 리스트
- address(list[k]) = address(list[lower_bound]) + ((k - lower_bound) * element_size)
> e.g. a: int, int: 4byte<br/>
a[0]의 주소가 0x10일 때, a[3]의 주소?<br/>
4*3 = C -> **0x1C**

### 다차원 배열

- 하드웨어 메모리는 선형적임
- 다차원 배열을 1차원 메모리로 사상시켜야 함
  - **행-우선 순서(row major order)**
  > 3  4  7<br/>
  6  2  5<br/>
  1  3  8<br/>
  -> 3, 4, 7, 6, 2, 5, 1, 3, 8의 순서로 저장됨
  - **열-우선 순서(column major order)**
  >-> 3, 6, 1, 4, 2, 3, 7, 5, 8의 순서로 저장됨
  
>e.g. supscript range lower bound = 0<br/>
다차원 배열 a는 row major order를 따름, int type<br/>
lower bound의 주소는 0x00010<br/>
a[2,3]의 주소는? -> 0x00038<br/><br/>
![스크린샷 2021-02-17 오후 11 41 35](https://user-images.githubusercontent.com/63772786/108220058-ad746500-7179-11eb-920f-7fabea3c320c.png)![스크린샷 2021-02-17 오후 11 41 48](https://user-images.githubusercontent.com/63772786/108220092-b6653680-7179-11eb-9686-431d94b93cbb.png)





<br/><br/><br/>
**참고 문헌**<br/>
Concepts of Programming Languages, Robert W. Sebesta -10th ed.<br/>
위키백과, https://ko.wikipedia.org/wiki/%EC%9C%A0%EB%8B%88%EC%BD%94%EB%93%9C