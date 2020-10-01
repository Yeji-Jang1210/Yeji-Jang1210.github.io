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

#### 메서드 정의
---

**인스턴스 메소드**
```swift
class Yeji{
    let name : String = "Yeji"
    var age : Int = 23   //stored property
    func myPrint(){ //Instance Method
        print("나이 : \(age), 이름 : \(name)")
    }
}

var jyg : Yeji = Yeji() //생성자 호출
//var jyg = Yeji()로 사용가능
print(jyg.name) 
jyg.myPrint()
```
위의 소스는 인스턴스 메소드를 만든 후 메소드를 호출하는 소스이다.  
함수를 호출하려면 생성자를 호출해야 하는데 생성자는 init로 만들지만 기본적으로 클래스를 만들면 `디폴트 생성자`가 자동으로 생성된다. 
클래스의 객체를 만들때는 뒤에 디폴트 생성자를 호출해야한다. 
<br><br>

**클래스메소드, 타입메소드**

```swift
class Yeji{
    let name : String = "Yeji"
    var age : Int = 23   //stored property
    func myPrint(){ //Instance Method
        print("나이 : \(age), 이름 : \(name)")
    }
    class func classMethod(){   //classMethod
        print("클래스 메소드입니다")
    }
    static func classMethod2(){
        print("클래스 메서드(static)입니다.")
    }
}
var jyg : Yeji = Yeji()
jyg.myPrint()
Yeji.classMethod()
Yeji.classMethod2()
```
클래스 메소드는 인스턴스가 아닌 클래스 자체가 사용하는 메소드로 jyg가 아닌 클래스.클래스메소드로 사용해줘야한다.  
클래스 키워드로 만든 클래스 메서드는 자식 클래스에서 override(부모 메서드에서 만든 클래스 메서드를 자식이 변형해서 사용)가 가능하다.
<br><br>

#### 프로퍼티 선언
---
프로퍼티는 저장 프로퍼티(stored property)와 계산 프로퍼티(computed property)가 있다.  

##### stored property
---

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
1. 옵셔널 변수(상수)로 선언한다. ex) var age : Int? (age는 옵셔널 변수로 초기값을 주지않아 nil이 들어간다.)
<br><br>

###### init
---
* init 메서드를 이용하여 생성자를 만들 수 있다.   

```swift
class Yeji{
    var name : String
    var age : Int   //stored property
    func myPrint(){ //Instance Method
        print("나이 : \(age), 이름 : \(name)")
    }
    init(myName : String, myAge : Int){
        name = myName
        age = myAge
    }//생성자
}
//var jyg : Yeji = Yeji() //오류
var jyg : Yeji = Yeji(myName : "YejiJang", myAge : 23)
jyg.myPrint()   //결과 :  이름 : YejiJang, 나이 : 23
```

* 생성자를 하나라도 만들 경우, default생성자를 호출할 경우 오류가 난다.  
<br><br>

###### failable initializer(실패 가능한 생성자 init? init!)
---

init 다음에 물음표(?)나 느낌표(!)를 사용하면 옵셔널 값이 리턴된다.  
ex)init?(name:String)  
ex)실패가능한 생성자가 있는 인스턴스 생성과 옵셔널 바인딩, 강제 언래핑  

```swift
class Yeji{
    var name : String
    var age : Int   //stored property
    func myPrint(){ //Instance Method
        print("이름 : \(name), 나이 : \(age)")
    }
    init?(name : String, age : Int){
      if age <= 0 {
        return nil
      }
      else
      {
        self.age = age
      }
        self.name = name
    }//생성자
}
//1)옵셔널 형 선언 후 옵셔널 바인딩
var yeji : Yeji? = Yeji(name : "Yeji" ,  age : 23)
if let yeji1 = yeji{
  yeji1.myPrint()
  }
//2)인스턴스 생성과 동시에 옵셔널 바인딩 많이사용
if let yeji2 = Yeji(name : "Yeji", age : 23) {
  yeji2.myPrint()
}
//3)인스턴스 생성 후 강제 언래핑
var yeji3 : Yeji = Yeji(name : "Yeji", age : 23)!
yeji3.myPrint()
//4)옵셔널 인스턴스를 사용시 강제 언래핑
if let yeji2 = Yeji(name : "Yeji", age : 23){
  yeji2.myPrint()
}
```
* 강제 언래핑의 방법 같은 경우 결과가 nil값을 반환한다면 위험하다(crash)  


###### self
---
다른언어 C++의 경우 this를 사용하였다면 swift는 C++의 this처럼 self를 사용하여 현재 클래스 내 메서드나 프로퍼티를 가리킬 때 사용한다.  
ex)    
```swift
class Yeji{
    var name : String
    var age : Int   //stored property
    func myPrint(){ //Instance Method
        print("나이 : \(age), 이름 : \(name)")
    }
    init(name : String, age : Int){
        self.name = name//name = myName
        self.age = age//age = myAge
    }//생성자
}
//var jyg : Yeji = Yeji() //오류
var jyg : Yeji = Yeji(name : "YejiJang", age : 23)
jyg.myPrint()   //결과 :  이름 : YejiJang, 나이 : 23
``` 
<br><br>

##### computed property
---
* computed property : 프로퍼티가 설정되거나 검색되는 시점에서 계산되거나 파생된 값을 말한다.
    * getter method : 값을 리턴
    * setter method : 값을 대입
ex)  getter만 있는 경우
```swift
class Yeji{
    var name : String //stored property
    var height : Double
    var cmHeight : Double{  //메서드 같지만 계산하는 프로퍼티다
        //get{
            return height*100
       // }
    }
    func myPrint(){ //Instance Method
        print("이름 : \(name), 키 : \(height)m")
    }
    init(name : String, height : Double){
        self.name = name//name = myName
        self.height = height
    }//생성자
}
var jyg : Yeji = Yeji(name : "YejiJang", height : 1.61)
jyg.myPrint()   //결과 : 이름 : YejiJang, 키 : 1.61m
print(jyg.cmHeight) //결과 : 161.0
```

<br>

ex)setter까지 있는 경우  
```swift
class Yeji{
    var name : String //stored property
    var height : Double
    var cmHeight : Double{  //메서드 같지만 계산하는 프로퍼티다
        get{
            return height*100
        }
        set(mHeight){
            height = mHeight * 0.01
        }
    }
    func myPrint(){ //Instance Method
        print("이름 : \(name), 키 : \(height)m")
    }
    init(name : String, height : Double){
        self.name = name//name = myName
        self.height = height
    }//생성자
}
var jyg : Yeji = Yeji(name : "YejiJang", height : 1.61)
print(jyg.cmHeight) //결과 : 161.0
jyg.cmHeight = 163.1
print(jyg.height)//결과 : 1.631
```
* setter을 사용한다면 getter은 생략할 수 없다.  
* 매개변수명은 newValue가 기본이다.  
    * newValue를 사용하면 setter의 매개변수를 생략할 수 있다.  
    ex)
    ```swift
    set{
            height = mHeight * 0.01
        }
    ```