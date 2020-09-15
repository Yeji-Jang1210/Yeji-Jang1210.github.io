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
    * **`nil`** : 값을 갖지 않는다는 의미의 값
        * `nil`은 기본 자료형에서 저장할 수 없기 때문에 옵셔널 타입으로 선언해야한다. 상수나 변수가 nil을 가지려면 옵셔널 타입으로 설정해야한다.  
        * Objective-C의 nil과는 다른의미 : 존재하지 않는 객체에 대한 <u>포인터(pointer)</u>  
        *출저)[swift vs Objective-C의 nil](https://you9010.tistory.com/232)*
    <br>   
* 옵셔널 타입을 사용하는 가장 큰 이유는, **옵셔널 타입만이 `nil`값을 가질 수 있기 때문이다.**  
    * 값을 입력받아야 하는 경우가 있을 때, 입력받아야 하는 자료형의 값이 아닌 아무것도 입력을 하지 않았을 경우를 대비하여 오류를 최소화 할 수 있기 때문이다.  

 ```swift
 var getNil = nil           //error
 var getNil : String = nil     //error
 var getNil : Int? = nil    //에러x
 var getNil : Int?          //에러x
 ```     

### 옵셔널 자료형 선언 방법
---
* 자료형 뒤에 `?`나 `!`를 붙여준다.  
ex)  
```swift
    var myNum : Int?  //옵셔널 정수형 myNum변수 선언     
    var myNum2 : Int!
    myNum = 8   //옵셔널로 '래핑되었다(wrapped)'라고 함
    myNum = 10
    print(myNum)
    //결과 : Optional(8) Optional(10)
```  
myNum의 자료형을 옵셔널 타입으로 지정했기 때문에 결과는 8이 아닌 **Optional(8)**,**Optional(10)**이 나오는 것이다.  
* `!` : swift4버전까지는 20이라고 나왔지만 5버전부터는 Optional(10)으로 나온다.    
    * 20이라고 나오는 이유 : `암묵적 언래핑(Implicitly unwrapping)`으로 선언했기 때문(아래 언래핑 방법 참조)
Optional()이 나오는 것이 싫다면 아래와 같이 강제로 옵셔널을 풀어주면 된다.(**`forced unwrapping(강제언래핑)`** 이라고 함) 
<br>

#### forced unwrapping(강제 언래핑)
---

1. **!**를 이용한 강제 언래핑  
ex)  
```swift
    print(myNum!)  //결과 : 8
```  
만약 myNum을 처음 선언할 때 값을 넣어주지 않으면 자동적으로 myNum변수는 `nil`이 된다.  
이 때, myNum을 forced unwrapping하려고 하면 오류가 나온다.(값이 없기 때문)  
ex)6
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

값을 넣지 않고 강제 언래핑 하는경우 if문을 이용해 오류를 막아주자.  
<br>

1. **Optional binding**  
옵셔널 바인딩은 느낌표 없이 옵셔널변수에 할당된 값을 임시 변수 또는 상수에 할당하여 값을 언래핑 할 수 있다.   
ex)  let 상수를 이용한 옵셔널바인딩 (여러개를 한번에 하는 방법)  
```swift
var myNum : Int?
var myNum2 : Int?
myNum = 8
myNum2 = 3
if let constantmyNum = myNum , let constantmyNum2 = myNum2
{
    print(constantmyNum, constantmyNum2)
}
else
{
    print("nil")
}
//결과 : 8 3
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
1. Implicitly unwrapping : 폐지
위에서 설명했던 것처럼 swift5버전으로 바뀌면서 폐지가 되었다.  
암묵적인 언래핑 방법으로 <u>클래스 초기화</u>에서 많이 사용되었었다.  
강제 언래핑이나 옵셔널 바인딩이 필요없이 값에 접근이 가능했다.  
ex)
```swift
var myNum : Int!
myNum = 8
//결과 : 8 / swift5 = Optional(8)
```
<br>

# 형변환 as? as!
---
<br>

## 형변환(Upcasting/Downcasting)
---
형변환은 상속관계가 있는 클래스들 끼리만 가능하다.  
 ![Image Alt 형변환]({{"/assets/img/posting/Study_iOS_img/Study_iOS_post3/형변환.png"| relative_url}}) 
1. Upcasting
    * Upcating이 안전한 이유 : 자식클래스는 부모클래스로부터 상속받아 많은 것을 가지고 있기 때문에 문제가 없다.  
    ex) 생물(부모)-사람(자식) => 사람은 생물이다.
1. Downcasting
    * 안전하지 않은 이유 : 부모 클래스는 자식클래스보다 많은 것을 가지고 있지 않음.  
    ex) 생물(부모)-사람(자식) => 생물은 사람이다.(동물도 있기때문 : 오류)

### as vs as? vs as!
---
as 연산자를 이용하여 타입변환(type casting)이 가능하다. 
 
|  | Upcasting | Downcasting |
| as   | 자식인스턴스 as 부모클래스 | as? : 성공 확신이 없을 경우 사용(변환 안되면 : crash)  ex) 부모인스턴스 <u>as!</u> 자식클래스 |
| | | as! : 성공 확신이 있을 경우 사용  ex) 부모인스턴스 <u>as?</u> 자식클래스 |
 

















