---
layout: post
title: "java복습-참조타입과 참조 변수"
featured-img: first-post
---
## 참조타입과 참조 변수

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

![Image Alt JVM메모리영역]({{"/assets/img/posting/JVM메모리영역.png"| relative_url}})

*JVM메모리 영역*
