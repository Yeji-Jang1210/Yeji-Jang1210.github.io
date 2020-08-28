---
layout: post
title: "java복습-클래스:객체지향 프로그래밍"
featured-img: emile-perron-190221
---

# 객체지향 프로그래밍
---
객체란?  
물리적으로 존재하거나 추상적으로 생각할 수 있는 것 중 자신의 속성을 가지고 있으면서 식별이 가능한 것이다.  
예를 들어 자동차라는 객체의 속성과 동작을 본다면  
자동차->[속성]: 색깔, 속도   [동작] : 달린다,멈춘다  
로 나눌수 있는데, 이것을 자바로 본다면 속성은 필드 동작은 메소드로 구분 할 수 있다.  
<br><br>

## 객체의 상호작용
---
소프트웨어에서 객체들은 각각 독립적으로 존재하고 **메소드**를 수단으로 이용해 상호작용을 한다.  
메소드 호출: 객체가 다른 객체의 기능을 이용하는 것  
```java
리턴값 = 객체.메소드(매개값1, 매개값2, ...);  
            ①               ②
```  
① : 객체에 점(.)을 붙이고 메소드 이름을 기술한다.  
        *점(.)*: 객체의 필드와 메소드에 접근할 때 사용한다.  

② : 매개값은 메소드를 실행하기 위해 필요한 데이터이다.  
    리턴값은 메소드 실행 후 호출한 곳으로 돌려주는(리턴하는) 값이다.  
<br>
예시를 본다면,  

```java
int result = Calculator.add(10,20);
```  
![Image Alt 객체의_상호작용]({{"/assets/img/posting/클래스_객체의상호작용.png"| relative_url}})  
<br>
이런 형식으로 사용을 하는데, Calculator객체의 메소드인 add에 매개값 10과 20을 대입하여 얻어낸 결과 30을 정수형(int) result(변수)에 되돌려준다.  

<br>
<br>

## 객체간의 관계
---
객체간의 관계는 **집합관계, 사용관계, 상속관계**로 나뉜다.  

![Image Alt 객체 간의 관계]({{"/assets/img/posting/클래스_객체간의관계.png"| relative_url}})  

1. **집합관계**
    집합관계에 있는 객체는 하나는 부품, 하나는 완성품에 해당한다.  
    ex)자동차: 엔진,타이어,핸들 등으로 구성 -> 자동차와 부품간의 관계 : 집합관계이다.
1. **사용관계**
    사용관계는 객체간의 상호작용을 말한다.  
    객체는 다른 객체의 메소드를 호출하여 원하는 결과를 얻어낸다.  
    ex)사람은 자동차를 사용 -> 사람은 자동차를 사용할 때 달림 -> 멈춘다,달린다 메소드를 사용 : 사용관계이다.  
1. **상속관계**
    상속관계는 **상위(부모)**객체를 기반으로 **하위(자식)** 객체를 생성하는 관계를 말한다.  
    ex)자동차는 기계의 한 종류이다. : 기계->상위객체, 자동차->하위객체

## 객체와 클래스
---
**클래스(Class)**
    설계도 역할을 한다. 클래스에는 객체를 생성하기 위한 필드, 메소드가 정의되어있음.  

**인스턴스(Instance)**
    클래스로부터 만들어진 객체를 해당 클래스의 인스턴스라고 함.  
    하나의 클래스로부터 여러 인스턴스를 만들 수 있음  
    ->*동일한 설계도로부터 여러 대의 자동차를 만드는 것과 동일*

<br>

객체 지향 프로그래밍 개발은 세가지 단계가 있다.
> * 1단계는 클래스를 설계
> * 2단계는 설계된 클래스를 가지고 사용할 객체 생성
> * 3단계는 생성된 객체 이용 

## 클래스 선언
---
1. **클래스 이름 정하기**  
    클래스는 한글이든 영어든 상관없지만 보통 영문을 사용하며 대문자로 시작한다.  
    ex) 
    ```
    Calculator, Car, Member, ChatClient, ChatServer, Web_Browser
    ```  
    잘못된 예) 3Car, $Car, _Car, int, for 

1. **소스파일 생성**  
    클래스 이름을 정했다면 **'클래스 이름.java'**소스 파일을 생성한다.  

    이클립스를 이용하여 클래스를 만드는 방법이다.  

    ![Image Alt 클래스생성_1]({{"/assets/img/posting/클래스생성_1.png"| relative_url}})  
    우측 마우스를 누르고 [New]-[Class]를 누른다.
    <br>
    <br>

    ![Image Alt 클래스생성_2]({{"/assets/img/posting/클래스생성_2.png"| relative_url}})  
    Class를 누르면 그림과 같은 화면이 나오는데 클래스 이름을 Name에 입력해준다.  

    <br>

    ![Image Alt 클래스생성_3]({{"/assets/img/posting/클래스생성_3.png"| relative_url}})  
    위 그림과 같이 .java가 자동으로 붙기 때문이다.  

    <br>
    
    클래스를 만들었으면 기본적으로 아래와 같이 나온다.
    ```java
    public class 클래스이름{

    }
    ```
    <br>
    일반적으로는 소스파일당 하나의 클래스를 선언하는데 아래와 같이 두개도 가능하다.
    ```java
    public class 클래스이름1{

    }
    public class 클래스이름2{

    }   //컴파일 시 클래스이름1과 클래스이름2가 각각 생성된다.
    ```  
    위의 소스를 컴파일 한다면 <u>바이트 코드 파일(.class)</u>는 클래스를 선언한 개수만큼 생긴다. 소스 파일은 클래스 선언을 담고 있는 저장 단위일 뿐, *클래스 자체는 아니다.*  

## 객체 생성과 클래스 변수
---
클래스로부터 객체를 생성하려면 아래와 같이 **new**연산자를 이용한다.  
```java
new 클래스();
```  
<br>

### new 연산자
    클래스로부터 객체를 생성시키는 연산자이다.  
    new 연산자 뒤에는 생성자가 오는데 생성자는 클래스()형태를 가지고 있다.    
<br>

클래스로 선언된 변수에 new 연산자가 리턴한 객체의 번지를 저장하는 소스이다.  
```java
클래스 변수;
변수 = new 클래스();
```  
<br>

아래와 같이 클래스 선언과 객체 생성을 1개의 실행문으로 작성할 수도 있다. 
```java
클래스 변수 = new 클래스();
```  
<br>

---

```java
public class Stduent{

}
```
<br>

```java
public class StudentExample{
    public static void main(String[] args){
        Student s1 = new Student();
    }
}
```
위의 소스에서 ***new연산자가*** 실행되는 과정이다.  

![Image Alt 클래스_new연산자]({{"/assets/img/posting/클래스_new연산자.png"| relative_url}})  
    1. new 연산자로 생성된 객체는 **메모리 힙(heap)영역**에 생성된다.  
    2. 객체를 생성시킨 후 객체의 **번지**를 리턴한다.  
    3. 이 주소를 **참조 타입인 클래스 변수**에 저장해두면 변수를 통해 객체 사용이 가능  
    *s1은 참조변수이므로 스택에 만들어진다.*
<br><br>

#### 클래스 선언
---  

```java
public class Student{

}
```
<br>

#### 클래스로부터 객체 생성
---

```java
public class StudentExample{
    public static void main(String[] args){
        Student s1 = new Student();
        System.out.println("s1변수가 Student 객체를 참조합니다.");

        Student s2 = new Stduent();
        System.out.println("s2변수가 또 다른 Student 객체를 참조합니다.");
    }
}
```  
> 결과  
![Image Alt StudentExample]({{"/assets/img/posting/StudentExample결과.png"| relative_url}})  
<br>

*※ s1과, s2는 new연산자를 통해 만들어 졌음으로 각각 다른 Student객체를 참조하고 있다.*  
지난 포스팅 참조 : [참조타입과 참조 변수](https://yeji-jang1210.github.io/java-study-first/)

<br>
 ※ Student 클래스는 라이브러리(API:Application Program Interface)용이고, StudentExample클래스는 실행 클래스 이다.  

 ```
    라이브러리 클래스 : 다른 클래스에서 이용할 목적(Student)
    실행 클래스 : 프로그램의 실행 진입점인 main()메소드를 제공하는 역할(StudentExample)
 ```  
<br>

라이브러리 클래스와 실행 클래스는  Student클래스 안에 main메소드를 작성하여 라이브러리인 동시에 실행 클래스로 만들 수도 있다. 

```java
public class Student{
    //라이브러리로서의 코드(필드,생성자,메소드)
    ...

    //실행 코드
    public static void main(String[] args){
        Student s1 = new Student();
        System.out.println("s1변수가 Student 객체를 참조합니다.");

        Student s2 = new Stduent();
        System.out.println("s2변수가 또 다른 Student 객체를 참조합니다.");
    }
}
```
*※위와 같이 작성 할 수 있지만 대부분의 객체지향 프로그램은 라이브러리와 실행 클래스가 분리되어 있다. 가급적이면 분리해서 작성하자*
  
<br><br>

## 클래스의 구성
---  
클래스 구성의 예시이다.  
```java
public class ClassName{

    //①필드
    int fieldname;

    //②생성자
    ClassName(){...}

    //③메소드
    void methodName(){...}
}
```  
<br>

1. __필드(Field)__
    객체의 데이터가 저장되는 곳이다.  
    선언형태는 변수와 비슷하지만, 필드를 변수라고 부르지는 않는다.  
    * 변수: 생성자와 메소드 내에서만 사용->생성자/메소드 종료시 **자동소멸**
    * 필드: 객체가 소멸되지 않는 한 **객체와 함께 존재**
<br>

1. __생성자(Constructor)__
    <u>new 연산자</u>로 호출되는 특별한 중괄호({}) 블록이다.  
    객체 생성시 초기화 역할 담당/메소드를 호출하여 객체 사용준비를 함  
    메소드와 비슷하게 생겼지만, **클래스 이름으로 되어있고 리턴형이 없음**
<br>

1. __메소드(Method)__
    객체의 동작에 해당하는 실행 블록(중괄호 블록{})  
    외부(호출한 곳)으로부터 매개값을 받아 실행에 이용하고, 실행 후 결과 값을 외부(호출한 곳)로 리턴해 줄 수도 있다.

<br><br>

*출저)혼자공부하는자바(한빛미디어)6-1객체지향프로그래밍.*       



