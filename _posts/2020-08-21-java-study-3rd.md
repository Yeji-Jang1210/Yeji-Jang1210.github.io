---
layout: post
title: "java복습-참조타입:열거타입"
featured-img: emile-perron-190221
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
<br>  
여기서 Week는 열거 타입으로 Week로 변수선언이 가능하다  
```java
Week today;
```  

<br>  

today 변수에 저장할 수 있는 것은 **Week에 선언된 7개의 열거 상수 중 하나**이다.  
```java
today = Week.FRIDAY;
```  
<br>
<br>

## 열거타입 선언  
---
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
<br>
<br>

## Eclipse에서 열거타입 추가하기
---
1. Package Explorer뷰에서 프로젝트 생성 후 [File]-[New]-[Enum]메뉴를 선택
    ![Image Alt 열거타입_추가1]({{"/assets/img/posting/enum_type추가.png"| relative_url}})
<br>

1. 아래와 같이 입력해주고 [Finish]버튼을 클릭한다.  
    ![Image Alt 열거타입_추가2]({{"/assets/img/posting/enum_type추가2.png"| relative_url}})  
    1. [Package] : 열거타입이 속할 패키지 이름을 입력
    2. [Name] : 열거타입의 이름을 입력

<br>
<br>

## 열거타입 변수
아래의 소스는 열거타입 변수의 선언과 열거 상수의 저장방법이다.  
형식 : 열거타입 변수 = 열거타입.열거상수;
```java
Week today;
today = Week.SUNDAY;

Week birthday = null;   //null값을 저장할수있음 : 참조타입이기 때문.
```  
*왜 열거타입은 참조타입일까?*  
    그 이유는 아래의 그림과 같다.

![Image Alt 열거타입과_참조타입]({{"/assets/img/posting/enum_type참조타입.png"| relative_url}})  

열거타입 변수 Week의 경우 MONDAY~SUNDAY까지의 열거 상수는 위의 그림과 같이 **총 7개의 Week 객체** 로 생성되고 메소드 영역에 생성된 열거 상수가 해당 Week 객체를 각각 **참조**하는 것이다.  
<br>
```java
Week today = Week.SUNDAY;
```  
![Image Alt 열거타입과_참조타입2]({{"/assets/img/posting/enum_type참조타입2.png"| relative_url}})

위의 소스의 today는 열거타입 변수로 스택영역에 생성이 된다 today에 저장되는 값은 Week.SUNDAY상수가 참조하는 **객체의 번지**이다. 따라서 아래의 소스의 연산 결과는 true가 된다.  
```java
today == Week.SUNDAY;   //true
```  

책에서 제공하는 확인문제의 2번을 풀어보자.  
```java
public class Exercise13 {
	public static void main(String[] args) {
		LoginResult result = LoginResult.FAIL_PASSWORD;
		if(result == LoginResult.SUCCESS) {
		} else if(result == LoginResult.FAIL_ID) {
		} else if(result == LoginResult.FAIL_PASSWORD) {
		}
	}
}
```  
이 소스를 사용하려면 열거타입을 어떻게 만들어야할까?  
1. 소스가 있는 패키지 안에 열거타입을 추가해준다. 위의 소스에서 열거타입의 이름은 LoginResult로 주어졌음으로 이 이름을 사용한다.  
    ![Image Alt 열거타입_문제1]({{"/assets/img/posting/확인문제2_1.png"| relative_url}})  
    <br>
1. result의 값은 LoginResult의 열거 상수가 주어지므로 아래와 같이 적어준다.  
    ![Image Alt 열거타입_문제2]({{"/assets/img/posting/확인문제2_2.png"| relative_url}})  
    <br>
1. 아래의 결과를 확인하기 위해 System.out.println을 사용하여 결과를 확인한다.  
    ![Image Alt 열거타입_문제1]({{"/assets/img/posting/확인문제2_3.png"| relative_url}}) 

<br>
<br>
<br>

*출저)혼자공부하는자바(한빛미디어)5-3열거타입.*




