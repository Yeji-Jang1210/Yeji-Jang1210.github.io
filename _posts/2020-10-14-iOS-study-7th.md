---
layout : post
title : "iOS공부 : 07주차"
featured-img: ios-study
categories : [iOS]
---
# 프로토콜(protocol)
---
* 특정 클래스와 관련없는 프로퍼티와 <u>메서드 선언</u>의 집합이다.  
    * 함수에 대한 정의가 아닌 <u>선언의 집합</u>이다.  
    * 기능이나 속성에 대한 설계도  
    * 클래스(구조체,열거형)에서 `채택`하여 메서드를 꼭 구현해야 한다.  
* Java나 C#의 인터페이스같은 역할
* C++의 abstract base class역할을 한다.(추상 부모 클래스)  
* **Protocol Oriented Programming(POP)** : 프로토콜 단위로 묶어 표현한 것, extension으로 기본적인 것을 구현하여 swift상속의 단점인 단일 상속의 한계를 극복한다.  
ex)   

```swift
class Child : ParentsClass, Protocol1, Protocol2 {

}
```  

스위프트에서 상속은 단일상속밖에 불가능하며, 부모클래스 뒤에 온 클래스들은 프로토콜이다.  
클래스, 구조체, 열거형, extension에 프로토콜을 `채택(adopt)`할수있음.  <br><br>

## 프로토콜의 정의
---
```swift
protocol ProtocolName {
    //프로퍼티 명
    //메서드 선언(선언만 되어있다.)
}
protocol ProtocolChild : ProtocolParents1, ProtocolParents2{
    //프로토콜은 다중상속이 가능하다. 
}
```
프로토콜을 사용하는 예시이다.  
```swift
protocol Activeable{
    var num : Int {get set} //get과 set은 선언만 있어도 동작을 한다.  
    func active()
}
class Man : Activeable {    //채택, adopt
    var num : Int = 1       //준수, conform
    func active(){ print("active") }    //준수, conform
}   //Protocol에 선언한 내용을 정의한다.  
var yeji : Man = Man()
yeji.active()   //active
print(yeji.num) //1
```
**클래스 안에 정의하면 되지 왜 프로토콜을 사용하나?**  
클래스에 선언 한다면 A,B의 클래스의 기능을 모두 상속받고 싶지만 swift에서는 단일 상속만이 가능하기 때문에,  
프로토콜을 채택하여 클래스에 구현하면 여러 기능을 사용할수 있다.  
