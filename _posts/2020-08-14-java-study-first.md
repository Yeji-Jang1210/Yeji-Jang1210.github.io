---
layout: post
title: "java복습-참조타입과 참조 변수"
featured-img: first-post
---
### 참조타입과 참조 변수

자바는 크게 기본타입과 참조타입으로 분류된다.

기본타입: 정수, 실수, 문자, 논리 *리터럴*을 저장하는 타입

->*리터럴*:변수에 넣는 변하지 않는 **데이터**를 의미한다.

**참조타입**: 객체(object)의 번지를 참조하는 타입으로 배열, 열거, 클래스, 인터페이스를 말한다.

기본타입과 참조타입의 변수의 예시를 봐보자.

```java
int age = 23;   //기본타입
String name = "장예지";     //참조타입
```
기본타입의 정수형 변수인 age는 직접 값을 저장하지만

String 타입인 name변수는 힙영역의 String객체 번지 값을 가지고 있다.

![Image Alt 참조타입]({{"/assets/img/posting/참조타입객체.png"| relative_url}})

*메모리에서 변수들이 갖는 값*

## JVM메모리 영역
JVM에서는 운영체제에서 할당받은 메모리 영역을 다음과 같이 세부 영역으로 구분해서 사용한다.
![Image Alt JVM메모리영역]({{"/assets/img/posting/JVM메모리영역.png"| relative_url}})

1. 메소드 영역
JVM에 시작할 때 생성되고 모든 스레드가 공유하는 영역.

코드에서 사용되는 클래스들을 클래스 로더로 읽어 클래스별로 정적필드와 상수, 메소드코드, 생성자 코드 등을 분류해서 저장

1. 힙 영역
객체와 배열이 생성되는 영역. 힙 영역에서 생성된 객체와 배열은 JVM스택 영역의 변수나 다른 객체의 필드에서 참조. 만약 참조하는 변수나 필드가 없으면 의미없는 객체가 됨으로 쓰레기 수집기(Garbage Collector)를 실행시켜 자동으로 제거한다.

1. JVM스택영역
JVM스택은 메소드를 호출할 떄마다 프레임(Frame)을 추가(push)하고 메소드가 종료되면 해당 프레임을 제거(pop)하는 동작을 수행한다.


## null과 NullPointerException

참조타입 변수는 힙 영역의 객체를 참조하지 않는다는 뜻으로 null(널) 값을 가질 수 있다.

null값도 초기값으로 사용할 수 있기 때문에 null로 초기화된 참조 변수는 스택 영역에 생성된다.

다음 그림은 참조 변수가 null값과 참조하는 값을 가르키는 것이다.

![Image Alt null_nullpointerException({{"/assets/img/posting/null_nullpointExcetpion.PNG"| relative_url}})

참조타입이 null을 가르키는지 확인하는 연산

```java
refVar1 == null //결과:false
refVar1 != null //결과:true

refVar2 == null //결과:true
refVar2 != null //결과:false
```
# NullPointerException
참조타입 변수를 잘못 사용하면 발생하는 **예외(Exception)**이다.

**예외(Exception)** : 프로그램 실행 도중에 발생하는 오류

```java
int[] intArray = null;
intArray[0] = 10; //NullPointerException예외 발생
```

intArray변수는 참조변수인데 null값으로 초기화가 되어있다.

위의 상태에서 intArray[0]에 10을 저장하려고 하면 NullPointerException이 발생한다 : 참조하는 배열 객체가 없기 때문

## String 타입

다음 아래의 소스를 봐보자

```java
String name1 = "장예지";
String name2 = "장예지";
String name3 = new String("장예지");
```
![Image Alt String객체 ({{"/assets/img/posting/String객체.PNG"| relative_url}})

# name1==name2의 결과는 *true* 이다.

name1과 name2는 동일한 문자열 리터럴로 생성된 객체를 참조하기 때문

java에서는 문자열 리터럴이 동일하다면 String객체를 공유하게 되어있다.

# name1==name3의 결과는 *false* 이다.

new 연산자로 만들어진 String 객체는 힙 영역에 새로운 객체를 만들때 사용하는
**객체 생성 연산자** 이기 때문이다.

만약 동일한 문자열인지 비교하고 싶은 경우에는 **equals() 메소드** 를 사용한다.
예시) 원본문자열.equals(비교문자열);
```java
boolean result = name1.equals(name3);
```
