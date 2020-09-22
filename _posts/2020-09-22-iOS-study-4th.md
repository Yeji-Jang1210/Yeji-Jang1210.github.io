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
    ```
    print(type(of:myNameAge))//결과 : (String, Int) -> String
```




