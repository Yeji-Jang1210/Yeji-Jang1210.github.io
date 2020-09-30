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
