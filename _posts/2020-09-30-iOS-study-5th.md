---
layout : post
title : "iOS공부 : 05주차"
featured-img: ios-study
categories : [iOS]
---
# 클래스(Class)
---
## swift의 객체지향 클래스
---
java와 c#에서는 클래스 안에서 선언되는 멤버 변수를 필드(Field), 동작하는 기능을 메소드(Method)라고 하는데,  
swift에서는 필드를 **프로퍼티(Property:속성)**, 메소드는 메소드(Method)라고 한다.  
<br><br>

### 클래스의 선언
---
swift에서 클래스를 선언하는 방법은 아래와 같다.  
```swift
class ClassName : ParentsClass {
    //Property
    //Instance Method
    //Type Method(Class Method)
}
```  
**`ParentsClass`** : 자바의 경우 extends를 쓰는데 swift에서는 extends대신 `:`을 사용한다.  
**`Property`** : 클리스 내 포함되는 변수와 상수를 정의한다.  
**`Instance Method`** : <u>객체</u>가 호출하는 메서드 정의  
**`Type Method`** : <u>클래스</u>가 호출하는 메서드 정의  
<br><br>

#### 프로퍼티 선언
---
프로퍼티는 저장 프로퍼티(stored property)와 계산 프로퍼티(computed property)가 있다.  
```swift
class Yeji{
    let name : String
    var age : Int   //stored property
}
```
저장 프로퍼티는 클래스안에 있는 일반적인 프로퍼티를 말한다.  
저장 프로퍼티는 초깃값을 주지 않으면 에러가 위의 소스가 그 경우이다.  
초기값을 주는 방법은,  
1. 초기값을 준다. ex)var age : Int = 23  
1. init을 이용하여 초기화한다.  
1. 옵셔널 변수(상수)로 선언한다.  