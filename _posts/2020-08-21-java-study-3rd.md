---
layout: post
title: "java복습-열거타입"
featured-img: 3rd-post
---
# 열거타입
열거타입은 한정된 값인 **열거상수(enumeration constant)**중에서 하나의 상수를 저장하는 타입이다.  
```java
public enum Week{   //WEEK:열거타입 이름
    MONDAY,
    TUESDAY,
    WEDNESDAY,
    THURSDAY,
    FRIDAY,
    SATURDAY,
    SUNDAY      //MON~SUN:열거 상수
}
```
여기서 Week는 열거 타입으로 Week로 변수선언이 가능하다  
```java
Week today;
```  
today 변수에 저장할 수 있는 것은 **Week에 선언된 7개의 열거 상수 중 하나**이다.  
```java
today = Week.FRIDAY;
```  

## 열거타입 선언  
열거타입을 선언하려면 해당이름으로 소스파일(.java)을 생성해야한다.  
보통 앞글자는 대문자로 쓴다.  
열거타입 선언에 enum은 **반드시 소문자로 적어야한다**  
```java
public enum 열거타입이름 {...}
```  
열거 상수는 모두 **대문자**로 표기하고 구성된 단어가 길경우 사이에 **밑줄(_)**로 연결해야한다.  
밑줄로 연결한 예시)  
```java
public enum LoginResult{ LOGIN_SUCCESS, LOGIN_FAILD }
```  





