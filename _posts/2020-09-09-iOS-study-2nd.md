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




