---
layout : post
title : "iOS공부 : 04주차"
featured-img: ios-study
categories : [iOS]
---

# 함수&Method/Closure
---
<br>

## 함수
---
* 소프트웨어에서 특정 동작을 수행하는 일정 코드 부분을 의미
* 수행을 위해 데이터가 제공, 작업결과를 반환할 수도 있음
* 하나의 큰 프로그램을 여러 부분으로 나누어주기 때문에 <u>같은 함수를 여러 상황에서 여러 차례 호출</u>할 수 있으며 일부분을 수정하기 쉽다는 장점을 가진다.
    * 출저)[함수-프로그래밍](https://ko.wikipedia.org/wiki/%ED%95%A8%EC%88%98_(%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D))
    <br>
* 함수에는 **`매개변수(parameter,인자)`**값과 **`아규먼트(argument,인수)`**값이 있다.
    * **`매개변수(parameter,인자)`** : 함수의 정의부에 있는 값으로 전달된 아규먼트를 받아들이는 변수이다.    
    * **`아규먼트(argument,인수)`** : 함수를 호출할 때 사용되는 값을 말한다.  
        ```c++
        void printFunction ( string parameter ){    //parameter,형식 매개변수
            print("%s",parameter);
        }
        int main(){
            printFunction( "argument" );   //"hello"는 실 매개변수
            return 0;
        }
        ```
<br>

## Method
---
스위프트에서는 함수를 클래스 내에 정의/선언하면 Method라고 부른다.  
클래스 말고도 구조체, 열거형(enum)안에 정의된 함수도 Method라고 한다.  <br><br>

## 함수의 선언
---
스위프트에서 함수를 선언하는 방법이다.  
```swift
func methodName( parameterName : parameterType ,...) -> returnType
{
    //methodCode
}
methodName( parameterName : argument ...)
```  
* `func` : 함수라는 것을 컴파일러에게 알려주는 키워드이다. 함수를 만들때 맨 앞에 사용  
* `methodName` : 함수의 이름으로 보통 낙타표기법을 사용한다.  
* `parameterName` : 매개변수의 이름
* `parameterType` : 함수에 전달되는 매개변수 타입
* `returnType` : 함수가 반환하는 결과 데이터의 타입  
    * 반환하지 않음 : Void
    * 반환값 타입(Void)과 `->`는 생략이 가능하다.
* `methodName( parameterName : argument ...)` : 스위프트에서는 형식 매개변수가 있는 메소드에서는 메소드를 호출할 때, <u>형식매개변수이름 : 인수값</u> 형식으로 사용한다.     
  
ex)swift함수
```swift
func myNameAge( myName : String, myAge : Int) -> String
{
    return ("내 이름은 \(myName), 나이는 \(myAge)세 입니다.")
}
let m = myNameAge(myName : "장예지", myAge : 23)   //return값을 상수 m에 대입
print(m) 
//결과 : 내 이름은 장예지, 나이는 23세 입니다
```  
<br><br>

### 외부,내부 매개변수
---
```swift
func myFunc(outParameter inParameter : Int, outParameter2 inParameter2 : Int) -> Int{
    return(inParameter + inparameter2)  //outParameter사용시 오류
}
let a = myFunc(outParameter:10, outParameter2:20)   //inParameter사용시 오류
```
* **`외부 매개변수`** : 함수를 호출할때 사용하는 매개변수
* **`내부 매개변수`** : 함수안에서 사용되는 매개변수
<br>

* **외부 매개변수는 생략이 가능하다.**    
1. 외부 매개변수를 적지 않는 방법
    ```swift
    func myNameAge( myName : String, myAge : Int) -> String
    {
        return ("내 이름은 \(myName), 나이는 \(myAge)세 입니다.")
    }
    ```
1. 외부 매개변수 이름 대신 `_`를 사용  
    ```swift
    func myNameAge( _ inMyName : String, _ inMyAge : Int) -> String
    {
        return ("내 이름은 \(inMyName), 나이는 \(inMyAge)세 입니다.")
    }
    let m = myNameAge( inmyName : "장예지", myAge : 23)   
    print(m) 
    ```
    * `_` : 외부 매개변수명을 생략하는 기호
    * **첫번째 외부 매개변수만 생략하는 경우가 많다.**
<br><br>

### type(of:메소드)
---
2주차에서 배웠던 type(of:변수명)은 메소드에도 사용이 가능하다.
ex)  
```swift
    func myNameAge( myName : String, myAge : Int) -> String
    {
        return ("내 이름은 \(myName), 나이는 \(myAge)세 입니다.")
    }
    print(type(of:myNameAge))//결과 : (String, Int) -> String
```
<br><br>

### 디폴트 매개변수(argument) 정의
---
매개변수를 2개 입력해야하는데 하나만 입력하고 싶은경우 함수를 선언할 때, **매개변수에 디폴드 값을 할당한다**
ex)
```swift
func myNameAge( myName : String="장예지", myAge : Int) -> String
    {
        return ("내 이름은 \(myName), 나이는 \(myAge)세 입니다.")
    }
let x = myNameAge(myAge : 23)    
print(x) //결과 : 내 이름은 장예지, 나이는 23세 입니다.
```
<br><br>

### 여러개의 결과 반환
---
여러 결과 값들을 `튜플`로 감싸서 반환할 수 있다.  
ex)
```swift
import Foundation
func sss(x :Int, y :Int) -> ( sum :Int, sub :Int, div :Double, mul :Int){
let sum = x+y
let sub = x-y
let div =Double(x)/Double(y)
let mul = x*y
return(sum, sub, div, mul)
}
var result = sss(x :10, y :3)
print(result.sum)
print(result.sub)
print(String(format:"%.3f", result.div))    //소수점 3자리수까지 출력
print(result.mul) //결과 : 13 7 3.333 30
```
### 가변 매개변수(variadic parameter)
---
함수에 올 매개변수의 수가 정해지지 않을 때 `...`을 사용하여 선언한다.  
ex)
```swift
func add(numbers:Int...){
  var sum : Int = 0
  for num in numbers{
    sum += num
  }
  print(sum)
}
add(numbers:1,2,3,4,5)  //결과:15
```
<br>

### inout 매개변수 : call by reference
---
swift는 대부분 call by value이지만 cal by reference로 함수가 값을 반환한 후에도 매개변수의 값을 유지하려면 형식 매개변수의 뒤에 inout을 붙여준다.  
ex)  
```swift
var myValue = 10
func doubleValue (value: inout Int) -> Int {    //call by reference로 받는다.
value += value
return(value)
}
print(myValue)
print(doubleValue(value : &myValue))  //함수에 myValue의 주소값을 넘겨줌
print(myValue) //출력 값 : 10 20 20
```
<br><br>

### 함수의 매개변수 사용
---
swift에서는 함수를 데이터 타입처럼 처리 할 수 있는데,  
ex) 
```swift
func inchesToFeet (inches: Float) -> Float {
return inches * 0.0833333
}
let toFeet = inchesToFeet //함수를 자료형처럼 사용
var result = toFeet(10) //inchesToFeet(inches : 10) : 함수호출시 함수이름이 아닌 상수 이름을 이용하여 호출함 
print(type(of:toFeet)) //결과 (Float) -> Float
```
* 특징
    * 변수에 저장이 가능하다.  
        ```swift
        let toFeet = inchesToFeet
        ```
    * 매개변수로 전달할 수 있다. 
        ```swift
            func outputConversion(converterFunc:(Float) ->Float,value : Float){
                let result = converterFunc(value)
                print("Result = \(result)")
            }
            outputConversion(converterFunc:toFeet, value: 10)
            
        ``` 
        * 첫번째 줄에서 converterFunc의 자료형으로 (Float)->Float 라는 부분으로 함수가 들어간다는 것을 알 수 있음
        * 마지막줄에서 converterFunc는 위의 toFeet 즉 inchesToFeet함수를 호출하여 불러온다.
    * 리턴값으로 사용할 수 있다.  
        ex)
        ```swift
        func returnfunction ( feet : Bool )->(Float){}->Float //(Float)->Float는 함수이고 리턴되는값이다.
        ```
    <br><br>   

## 함수명
---
* 함수명은 `함수명(외부매개변수:외부매개변수:...)`이다. 
<br>

* 외부매개변수가 없을 경우
```swift
    func myNameAge( myName : String, myAge : Int) -> String
    {
        return (" \(myName), \(myAge)")
    }
```
위의 함수는 외부 매개변수가 없는 함수이다.  
따라서 함수명은 `myNameAge(::)`라고 쓴다.  

* 두번째 매개변수부터 이름이 있을 경우
```swift
    func myNameAge( _ inMyName : String, myAge inMyAge : Int) -> String
    {
        return ("내 이름은 \(inMyName), 나이는 \(inMyAge)세 입니다.")
    }
```
위의 함수명은 `myNameAge(_:myAge:)`이다.  
<br><br>

## 클로저
---
클로저는 이름이 없는 `익명함수`라고 한다.  
```swift
func add(a : Int, b : Int)->Int{
    return(a+b)
}
print(add(a:10, b:10))//결과 : 20
```
위가 일반함수라면, 클로저는 아래와 같이 사용한다.  
```swift
let add1 = { (a : Int, b : Int)-> Int in return(a+b) }
print(add1(10,10))//결과 : 20
```
* 일반함수에서 클로저 표현식으로 표현하는 방법  
    1. 상수를 적고 함수 이름을 없앤다.  
    2. 함수이름을 없앤 뒷부분을 중괄호 안에 넣어준다.
    3. **`in`**을 사용한 뒤 리턴값을 적어준다.  
    4. print할때에는 인수 값만 적어준다.   
    <br><br>

```swift
func printHello(){
    print("hello")
}
printHello()
```
위의 함수를 더 간단하게 아래와 같이 나타낼 수도 있다.  
```swift
let sayHello = { print("Hello") }
sayHello()
```
<br><br>

### 후행 클로저(trailing closure)
---
클로저가 함수의 마지막 인자(argument)라면 마지막 매개변수 이름을 생략 후 함수 소괄호 외부에 구현한다.  
* 클로저 축약 및 예제
```swift
let fruits = {(fruit:String, fruit2:String)->String in return("과일:\(fruit),\(fruit2)")}
var result = fruits("사과","바나나")
//print(result)

let animals = {(animal:String, animal2:String)->String in return("동물:\(animal),\(animal2)")}
var result2 = animals("고양이","강아지")
//print(result2)

func kinds(object:String, object2:String, kind: (String, String)-> String) -> String {
  return kind(object,object2)
}
result = kinds(object : "키위",object2 : "오렌지", kind : fruits)
//print(result)

result = kinds(object : "키위", object2 : "오렌지", kind : {(fruit:String, fruit2:String) -> 
String in return("과일:\(fruit),\(fruit2)")
 })
//print(result)

result = kinds(object : "키위", object2 : "오렌지", kind : {(fruit:String, fruit2:String) in return("과일:\(fruit),\(fruit2)")
 })
//print(result) //리턴형 생략

result = kinds(object : "키위", object2 : "오렌지", kind : { return("과일:\($0),\($1)")
 })
//print(result) //매개변수 생략 후 단축인자 사용

result = kinds(object : "키위", object2 : "오렌지")
 { return("과일:\($0),\($1)")}
//print(result) //매개변수 생략 후 단축인자 사용

result = kinds(object : "키위", object2 : "오렌지",
 kind: { "과일:\($0),\($1)" })
//print(result) //마지막 줄을 리턴하므로 return 생략

result = kinds(object : "키위", object2 : "오렌지"){ "과일:\($0),\($1)" }
print(result) //return 생략


```