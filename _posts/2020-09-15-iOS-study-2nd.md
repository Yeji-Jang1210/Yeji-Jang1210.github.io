---
layout : post
title : "iOS공부 : 03주차"
featured-img: ios-study
categories : [iOS]
---

# Optional 1
---
<br>

```swift
print(Int("100"))   //결과 : Optional(100)
```
문자 100을 정수형으로 출력하려고 하면 결과는 [Optional(100)]이라는 결과가 나온다.  Optional은 무슨 뜻일까?  
<br>

## Optional(옵셔널)/Optional Type 이란?
---
* Swift언어에 있는 새로운 개념으로, 자료형의 값을 저장하거나 **`nil`**을 저장 할 수 있다.  
    * **`nil`** : 값이 없는 것 
    * nil은 기본 자료형에서 저장할 수 없기 때문에 옵셔널 타입으로 선언해야한다.
    <br>   

### 옵셔널 자료형 선언 방법
---
* 자료형 뒤에 `?`를 붙여준다.  
ex)  
```swift
    var myNum : Int?  //옵셔널 정수형 myNum변수 선언     
    myNum = 8   //옵셔널로 '래핑되었다(wrapped)'라고 함
    print(myNum)
    //결과 : Optional(8)
```  
myNum의 자료형을 옵셔널 타입으로 지정했기 때문에 결과는 8이 아닌 **Optional(8)**이 나오는 것이다.  
Optional()이 나오는 것이 싫다면 아래와 같이 강제로 옵셔널을 풀어주면 된다.(**`forced unwrapping(강제언레핑)`** 이라고 함) 

#### forced unwrapping(강제 언레핑)
---

1. **!**를 이용한 강제 언레핑  
ex)  
```swift
    print(myNum!)  //결과 : 8
```  
만약 myNum을 처음 선언할 때 값을 넣어주지 않으면 자동적으로 myNum변수는 `nil`이 된다.  
이 때, myNum을 forced unwrapping하려고 하면 오류가 나온다.(값이 없기 때문)  

```swift
var myNum : Int?    //옵셔널 정수형 myNum선언
myNum = 8
if myNum != nil {   //띄어쓰기 주의! myNum! =nil로 인식할 수 있음
    print(myNum!)
}
else {
    print("Is nil")
}
//결과 : 8
```  

값을 넣지 않고 강제 언레핑 하는경우 if문을 이용해 오류를 막아주자.  
<br>

1. **Optional binding**  

옵셔널 바인딩은 느낌표 없이 옵셔널변수에 할당된 값을 임시 변수 또는 상수에 할당하여 값을 언레핑 할 수 있다.   
ex)  let 상수를 이용한 옵셔널바인딩  
```swift
var myNum : Int?
myNum = 8
if let constantmyNum = myNum 
{
    print(constantmyNum)
}
else
{
    print("nil")
}
//결과 : 8
```  
ex) var 변수를 이용한 옵셔널 바인딩
```swift
var myNum : Int?
if var variablemyNum = myNum 
{
    print(variablemyNum)
}
else
{
    print("nil")
}
//결과 : nil
```  

















