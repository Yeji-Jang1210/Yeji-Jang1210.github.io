---
layout : post
title : "iOS공부 : 06주차"
featured-img: ios-study
categories : [iOS]
---
# 상속(Inheritance)
---
상속은 객체 지향 프로그래밍을 구성하는 중요한 특징 중 하나로,  
1) 높은 수준의 코드 재활용성을 제공하며,   2) 클래스 간 계층적 관계를 구성하여 다형성의 문법적 토대를 마련한다.  
<br><br>

## 상위클래스(Super Class)와 하위 클래스(Sub Class)
---
**상위 클래스**는 슈퍼클래스 혹은 부모클래스(Parent class)라고 불린다.  
**하위클래스**는 부모클래스에게서 상속받은 클래스를 말하며 자식클래스(Child Class)라고도 한다. swift에서 부모클래스는 **`단일 상속(single inheritance)`**의 특징을 가진다.  
**`단일 상속(single inheritance)`** :  **하위클래스 하나당 단 하나의 부모클래스만 상속이 가능하다.**    

## swift의 상속 방법
---
아래 소스는 스위프트의 상속 방법이다.  
```swift
class Child : Parent , protocol1 {
    //부모 클래스는 하나만 상속 가능
    //콜론 다음이 여러 개이면 나머지는 프로토콜이다.  
}
```
swift에서의 상속은 **클래스**만 가능하고, 부모명 옆에 `프로토콜`명을 적어주고, 부모클래스가 없을 경우에는 바로 프로토콜 명을 적어주면 된다.  
ex) class Child : protocol1 { }  <br>

상속의 예시  
```swift
class Parent{
  var age : Int
  var name : String
  func printMe(){
    print("나이 : \(age), 이름 : \(name)")
  }
  init(age : Int, name : String){
    self.age = age
    self.name = name
  }
}

class Child : Parent{
  //비어있지만 부모클래스의 모든것을 가지고 있음
}
var choi :Parent = Parent(age : 50, name : "부모")
choi.printMe() // 나이 : 50, 이름 : 부모
var jang : Child = Child(age : 23, name : "자식")
jang.printMe() // 나이 : 23, 이름 : 자식
print(jang.age) // 23
```
Parent를 상속받은 Child클래스 내부에는 아무것도 선언이 되어있지 않은 것으로 보이지만, 부모로부터 상속받았기 때문에 부모의 클래스 내부의 내용이 들어가 있다.  
<br><br>
부모로 상속받은 생성자에 프로퍼티를 추가하고 싶은 경우에는 init 메서드를 수정해줘야한다.  

```swift
class Child : Parent{
 var height : Double = 161.3
 func printMe_h(){
    print("나이 : \(age), 이름 : \(name), 키 : \(height)cm")
 }
 init(age : Int, name : String, height : Double){
    super.init(age : age, name : name)
    self.height = height
  }
}
var jang : Child = Child(age : 23, name : "자식", height : 171.2)
jang.printMe_h() // 나이 : 23, 이름 : 자식, 키 : 171.2cm
print(jang.age) // 23
```
<br><br>

## Overriding(함수중첩)
---
부모로부터 받은 메서드가 마음에 들지 않은 경우 같은 함수 이름으로 새로운 메서드를 재정의하는 것을 말한다.   
```swift
class Child : Parent{
 var height : Double = 161.3
 override func printMe(){
    print("나이 : \(age), 이름 : \(name), 키 : \(height)cm")
 }
 init(age : Int, name : String, height : Double){
    super.init(age : age, name : name)
    self.height = height
  }
}
var jang : Child = Child(age : 23, name : "자식", height : 171.2)
jang.printMe() // 나이 : 23, 이름 : 자식, 키 : 171.2cm
```
부모 클래스는 상속의 예시부분에 적어놓은 클래스와 같고 위의 소스는 부모의 함수를 overriding한 것이다. 재정의할 함수 앞에 `override`를 적어주면 된다. 자식클래스에서 함수를 호출하면 부모클래스의 함수가 아닌 자식클래스에서 재정의한 함수가 호출된다.  