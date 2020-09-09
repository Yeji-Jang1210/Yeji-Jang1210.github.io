---
layout : post
title : "iOS공부 : 02주차"
featured-img: ios-study
categories : [iOS]
---

# 2주차 swift 문법1
---  
<br><br>

## swift란?
---  
Swift는 전화,  데스크톱, 서버 또는 코드를 실행하는 모든 것을위한 소프트웨어를 작성하는 환상적인 방법이다.  
[swift homepage](https://docs.swift.org/swift-book/index.html)  

Paradigm | protocol-oriented 기반 Multi-paradigm언어, 객체지향언어, 함수형언어이기도 하다.  
Designed by | 대표인물 : [Chris Lattner](https://en.wikipedia.org/wiki/Chris_Lattner)  
First appeared | 2014년 6월 2일  
Typing discipline | Statig, strong, inferred  
OS | macOS, Darwin, Linux, Windows, Android  
Influenced by | objective-C, Rust, Haskell, Ruby, Python, C#, CLU, D  

<br><br>

## 데이터 타입(자료형), 상수(let), 변수(var)
---

### 데이터 타입(자료형, date type)
* 스위프트 프로그램에서 숫자를 저장
    * var mynumber - 10  
        → *mynumber라는 이름의 변수를 생성했으며, 숫자 10을 할당한다.*  
    * var mynumber : **Int** = 10  
        → *위와 같이 초기값이 있을 경우에는 컴파일러가 타입 추론(type inference)을 하므로 데이터 타입을 명시할 필요가 없음* 
        → *자료형의 첫글자는 **대문자**로 써준다* 
    * 일반적으로 초깃값을 주지 않을 경우에만 자료형을 쓴다.  
        ```swift
        var welcomeMessage : String //초깃값이 x=>자료형 직접표기
        ```    
    ex)C언어  
    ```c
    int x = 10;
    ```
* 기본적인 자료형 : Bool, Character, Int, Float, Double, String, Void  
<br>

* **아래와 같이 작성하면 오류가 난다.**
    ```swift
    var x : Int
    x= 10
    //error '=' must have consistent whitespace on both sides, '=' 양쪽에 일관된 공백
    ```
    맞게 쓰려면 =사이에 공백을 꼭 해줘야한다 : x = 10
* 자료형의 종류와 크기가 궁금하다면?
    ```swift
    var x = 10
    print(type(of:x))
    let s = MemoryLayout.size(ofValue: x)
    let t = MemoryLayout<Int>.size
    print(s, t)
    ```
    * type(of:x) → x의 자료형을 알려줌  
    * MemoryLayout.size(ofValue: x) → x 변수의 크기가 몇인지 알려줌(byte)  
    * MemoryLayout<Int>.size → x의 크기가 몇인지 알려줌  

<br><br>

#### 정수형 데이터 타입 : Int
---
<br>

* 정수(소수점이 없는 수)를 저장하는데 사용한다.
* \ (출력하고 싶은 변수나 상수)
    ex)
    ```swift
    print("Int32 Min =\(Int32.min) Int32 Max = \(Int32.max)")  
    //결과 : Int32 Min = -2147483648 Int32 Max = 2147483647
    ```

<br><br>

#### 부동소수점형 데이터 타입 : Double
---
<br>

* 소수점이 있는 숫자이다.  
* **Float**와 **Double** 타입을 제공함
    * `Float` : 32bit로 부동 소수점 수를 저장, 소수점 6자리 정확도  
    * `Double` : 64bit로 부동 소수점 수를 저장, 소수점 15자리 정확도  
* Double 형이 기본이다.
    ex)
    ```swift
    var myWeight : Double 58.5  //초깃값에 소수점이 있음으로 Double은 일반적으로 생략한다.  
    ```    
<br><br>

#### 부울 데이터 타입 : Bool
---
<br>

* 참 또는 거짓(1 또는 0) 조건을 처리할 데이터 타입  
* Boolean 데이터 타입을 처리하기 위해 두 개의 불리언 상수값(true/false) 사용  
    ex)
    ```swift
    var orangesAreOrange : Bool = true
    //초깃값 true가 있음으로 Bool은 일반적으로 생략함
    ```  
<br><br>

#### 문자 데이터 타입 : Character
---
<br>    

* 문자, 숫자, 문장 부호, 심볼 같은 유니코드(Unicode) 문자 하나를 저장
    * 스위프트에서의 문자들은 문자소 묶음(grapheme cluster)의 형태로 저장
        *문자소 묶음은 하나의 문자를 표현하기 위해 유니코드 코드 값들로 이루어짐*
* var  변수명 : **Character** = "초깃값"  
    ※주의 : 초깃값은 작은 따옴표가 아니고 **큰따옴표**이다.  
    ex)
    ```swift
    var myChar :  Character = "X" //Character 생략불가 :  생략할경우 String 형임  
    ```        
* 유니코드를 이용하여 변수에 문자 'X'를 할당
    * ex) var myChar4 = "\ u{0058}"

<br><br>

#### 문자열 데이터 타입 : String
---
<br>

* 단어나 문장을 구성하는 **일련의 문자**
* 저장, 검색, 비교, 문자열 연결, 수정 등의 기능을 포함
* 문자열 보간(string interpolation)을 사용하여 문자열과 변수, 상수, 표현식, 함수 호출의 조합으로 만들 수도 있음
    ex)
    ```swift
    var userName : String = "Kim"
    var age = 20
    var message = "\(userName)의 나이는 \(age)입니다."
    print(message)
    //결과 : Kim의 나이는 20입니다.
    ```
<br><br>

#### 특수 문자/이스케이프 시퀀스
---
<br>

* 표준 문자 세트뿐만 아니라 문자열에 개행, 탭, 또는 유니코드 값과 같은 항목을 지정할 수 있는 여러 특수 문자도 있다.  
* 일반적으로 많이 사용되는 특수 문자
    * \n : 개행
    * \r : 캐리지 리턴(carriage return)
    * \t : 수평 탭
    * \ \ : 역슬래시
    * \" : 큰따옴표(문자열 선언문에 큰따옴표를 쓰고 싶을 경우 사용)
    * \u{nn} : nn위치에 유니코드 문자를 표현하는 두개의 16진수가 배치되는 1바이트 유니코드 스칼라
    * \u{nnnn} : 2바이트 유니코드 스칼라
    * \U{nnnnnnnn} : 4바이트 유니코드 스칼라

<br><br>

#### 변수 : var
---
<br>       

* 기본적으로 변수(variable)는 프로그램에서 사용될 데이터를 저장하기 위한 메모리 공간이다.  
* 변수에 할당된 값은 **변경이 가능**
    ex)
    ```swift
    var myVariable = 10
    var x = 0.0, y = 0.0, z = 0.0
    ```

<br><br>

#### 상수 : let
---
<br>

* 상수(constant)는 데이터 값을 저장하기 위하여 메모리 내의 명명된 공간을 제공한다는 점에서 변수와 비슷하다.  
* 어떤 값이 **한번 할당되면 이후에 변경이 불가능**
* 코드 내에서 반복적으로 사용되는 값이 있을 경우 유용하다.  
* 변수나 상수 명은 영문자, 숫자, Unicode(이모티콘, 중국어...)도 가능하다.  

<br>

**애플은 코드의 효율성과 실행 성능을 높이기 위해 변수(var)보다는 상수(let)를 사용하라고 권장함.**  

<br><br>

#### 타입 어노테이션(type annotation)과 타입 추론
---
<br>

* 스위프트는 타입 안전(type safe) 프로그래밍 언어이다.  
* 상수와 변수의 타입을 식별하는 방법은 두가지이다.  
    1. 변수 또는 상수가 코드 내에서 선언되는 시점에 **타입 어노테이션**을 사용하는 것  
    ex)
    ```swift
    var userCount : Int = 10    //Int가 타입어노테이션임
    ```
    1. 선언부에 타입 어노테이션이 없을경우 컴파일러는 상수 또는 변수의 타입을 식별하기 위해 **타입추론(type inference)** 사용함  
    해당 상수 또는 변수에 값이 할당되는 시점에서 그 값의 타입을 확인하고 그와 같은 타입처럼 사용한다.  
    ex)
    ```swift
    var userCount = 10 //Int형이라고 타입추론을 함
    ```
* 상수를 선언할 때도 타입 어노테이션을 사용하면 나중에 코드에서 값을 할당할 수 있다.  
* 이미 값이 할당되어있는데 다시 할당하려고 하면 에러가 남

<br><br>

#### 튜플(Tuple)
---
<br>

* 여러 값을 하나의 개체에 일시적으로 묶는 방법이다.  
* 튜플에 저장되는 항목들은 어떠한 타입도 될 수 있으며, 저장된 값들이 모두 동일한 타입이어야 한다는 제약도 없음
    ex)
    ```swift
    let myTuple = (10,12.1,"Hi")
    var myString = myTuple.2
    print(myString)
    //결과 : Hi
    ```
* 특정 튜플 값은 인덱스 위치를 참조하면 간단하게 접근이 가능하다.  
0부터 시작한다. 
* 무시하고 싶은 값은 밑줄(_)을 사용하면 그 값은 무시된다.   
