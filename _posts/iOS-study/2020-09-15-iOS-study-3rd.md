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
 
1. Upcasting  

|  | Upcasting |
| as | 자식인스턴스 <u>as</u> 부모클래스 |

1. Downcasting  

|  | Downcasting | 사용하는 방법 |
| **as!** | 부모인스턴스 <u>as!</u> 자식클래스 | 반드시 성공한다는 확신이 있을 때(강제변환 : forced conversion)/(변환 안되면 : crash) |
| **as?** | 부모인스턴스 <u>as?</u> 자식클래스 | 확신이 없을 경우 |  

※ `as?`로 Downcasting했을경우 **옵셔널타입**으로 변환된다.  

<br><br>

# 타입검사 (is)
---
* 인스턴스가 어떤 클래스인지 알고 싶을때 사용한다.  
    * is 키워드를 사용함 : 인스턴스 is 클래스
ex)    
```swift
class A { }       //클래스 생성
var a : A = A()  //A로부터 인스턴스 a를 만듬 A():디폴트 생성자
if a is A        //a가 A클래스인가?
{
    print("Yes")
}
```
<br><br>

# Any vs AnyObject(Protocol)
---
  
|          |   Any   |   AnyObject   |  
| 허용범위 | 클래스, 구조체,열거형 함수타입도 가능 | 클래스의 인스턴스만 가능(구조체,열거형 허용 x) |  
   
Any가 AnyObject보다 더 포괄적인 개념이다. 
* AnyObject 추가설명
    * 범용타입으로 상속관계가 아니라도 타입 캐스팅이 가능한 타입
    * 어떤 클래스의 객체도 저장이 가능하다.       

<br><br>

# 연산자
---   
swift에서 사용하는 연산자를 보자  

## 증가/감소 연산자
---
※swift3에서 x++,x--는 사라져서 사용이 불가하다.  
* x++ : x+=1, x = x+1을 사용  
* x-- : x-=1, x = x-1을 사용  

## 범위 연산자
---
1. 닫힌 범위 연산자(closed range operator)
    * x...y : x에서 시작해서 y로 끝나는 범위에 포함돈 숫자
        * ex) 1..5 : 1,2,3,4,5
1. 반 열린 범위 연산자(half-open range operator)
    * x..< y : x부터 시작하여 y가 포함되지 않는 모든 숫자
        * ex) 1..<5 : 1,2,3,4  
 1. One-Sided Ranges : 배열  
    * ex) 
    ```swift
    let names = ["A","B","C","D"]
    for name in names[2...]{
        print(name)
    }     //결과 : C D
    ```

## Nil-Coalescing Operator (Nil 합병 연산자) [??]
---
* 옵셔널 변수의 값이 nil 이면 `??` 다음 값으로 할당됨 
```swift
let defaultNum = "981210"
var classNum : String?
classNum = "201912038"
print(classNum)
var myClassNum = classNum ?? defaultNum
print(myClassNum)   //결과 : Optional("201912038") 201912038
```
classNum이 nil값이 아님으로 옵셔널이 풀려 그냥 String인 201912038이 나온다.  

만약 아래와 같이 classNum값이 nil이라면
```swift
let defaultNum = "981210"
var classNum : String?
//classNum = "201912038"
print(classNum)
var myClassNum = classNum ?? defaultNum
print(myClassNum)   //결과 : nil 981210
```
첫번째 print(classNum)에서는 nil값이 나오고,  
var myClassNum = classNum `??` defaultNum 문장에서  
classNum이 nil이므로 `??`뒤에있는 defaultNum값이 적용되어서 981210이라는 String값이나온다.  

<br><br>

# 반복문
---
배웠던 프로그래밍 언어들의 반복문과 swift언어에서의 반복문의 차이점을 보자  

## if문
---
* if문은 다른 프로그래밍 언어들과 다르게 반복할 문장이 한줄이어도 **`{}`**를 필수적으로 사용해줘야 한다.  
* else문도 if문과 마찬가지로 **`{}`**를 사용해줘야한다.  

### if문 if-else문
---

ex)c++의 경우  
```c++
int x = 5
if (x > 10)
    std::cout << "x는 10보다 큽니다.";
else 
    std::cout << "x는 10보다 작습니다.";   
//결과 : x는 10보다 작습니다. 
```
ex) swift의 경우
```swift
var x = 15
if (x > 10){
    print("x는 10보다 큽니다.")
}
else{
    print("x는 10보다 작습니다.")
}
//결과  : x는 10보다 큽니다.
```
<br>

### 다중 if-else문
---
다중 if-else문도 마찬가지로 else if 조건문 다음에 **`{}`**를 필수적으로 사용해야 한다.  
ex)  
```swift
var score = 78
if (score >= 90 && score <= 100){
  print("A입니다.")
}else if (score >= 80 && score < 90 ){
  print("B입니다.")
}else if (score >= 70 && score < 80 ){
  print("C입니다.")
}else {
  print("노력하세요")
}//C입니다.
```
<br>

### guard문
---
swift 2에 도입되어 **false**일 경우 **else절**을 반드시 포함해야한다.  
    * else절 안에는 return, break, continue, throw 구문을 반드시 포함해야한다.  
ex)
```swift
guard <불리언 표현식> else {
    //거짓일경우 실행될 코드
   <return, break, continue ,throw 등의 구문>
}
//참일경우 실행될 코드 
```    
<br>

## for-in 반복문
---
우리가 일반적으로 알고있는  
ex)  
```c++
for(int i=0 ; i<10 ; i++){
    //반복할문장
}
```
[for 초기화;조건;증감]은 swift 3에서 없어졌다.  
대신 **for-in** 반복문이라는 것이 나왔는데, 아래처럼 사용한다.  
```swift
for 상수명 in 컬렉션 또는 범위
{
    //실행될 코드
}
```  
* `상수명` : for-in 반복문이 돌면서 컬렉션 또는 범위에서 가져온 **항목을 담게 될 상수**를 말한다.  
* `컬렉션 또는 범위` : 반복문이 반보고디면서 현재 항목을 참조한다.  
ex)
```swift
for _ in 1...5{
    print("hello")
}
```
위의 for-in반복문처럼 i 변수 대신 **`_`** : 생략의 의미를 사용하여 간단하게 반복문을 돌릴 수 있다.  

ex) 배열을 이용한 for-in
```swift
let fruits = ["banana", "apple", "orange", "lemon"]
for fruit in fruits{
    print(fruit)
}
```
결과) 위의 for-in반복문 결과로는 fruits라는 배열의 항목들이 차례로 출력이 된다.   
```
banana
apple
orange
lemon
```    
<br>

ex)dictionary를 이용한 for-in
```swift
let fruitsNumber = ["banana" : 6, "apple" : 5, "orange" : 4, "lemon" : 3]   //dictionary는 key:value형식의 배열이다.
for (fruitName, number) in fruitsNumber{
    print("\(fruitName) : \(number)")
}
```
결과)  
```
banana : 6
apple : 5
orange : 4
lemon : 3
```  
<br><br>  

## while 반복문 
---
for문은 몇 번을 반복할지 정해져있을때 유용하지만 while문은 몇 번을 반복할지 정해져 있지 않을때 즉 조건이 만족할때까지 반복하는 경우 유용하다.  
ex)  
```swift
var myNum = 0
while myNum < 24 {
    myNum = myNum + 1
}
print(myNum)
```  
결과 : 24 (조건이 만족할 시점에 빠져나오므로 24가 나온다.)  

### repeat-while 반복문
---
do ... while 반복문을 대신하는 문으로 적어도 한번은 실행한다.  
ex)  
```swift
var i = 10
repeat {
  i=i-1
  print(i)
}while (i > 0)
```
결과)  
```
9
8
7
6
5
4
3
2
1
0
```
<br>

### break continue 문
---
`break`: 무한루프 혹은 반복문에서 빠져나오고 싶을 때 사용한다.  
ex)
```swift
for i in 1..<10{
    if i > 5 {  //무조건 중괄호 써줘야 함!
        break
    }
    print(i)
}   //결과 1 2 3 4 5
```
<br>

`continue` : continue 이후의 모든 코드를 건너뛰고 반복문의 상단 시작위치로 돌아갈때 사용한다.  
ex)
```swift
for i in 1...10{
    if i % 2 == 0 { //2로 나누어 나머지가 0일경우(짝수면)
        continue    //if 문 위로 올라간다.
    }
    print(i)    //결과 :  1 3 5 7 9
}
```  

### switch-case문
---
* 입력한 변수에 일치하는 case를 찾아 case아래의 문장이 실행된다. 
* 각 case문 안에는 **break**문이 자동적으로 숨어있다.  
* case문 안에 문장이 없을경우 오류가 나타난다.  
ex)
```swift
var day = 4
switch (day)
{
  case 1:
    print("월") 
  case 2:
    print("화") 
  case 3:
    print("수")
  case 4:
    print("목") 
  case 5:
    print("금")
  default : 
    print("주말입니다")          
}
//결과 : 목
```
case문에는 여러 변수들을 결합할 수도 있다.  
ex)
```swift
var day = 4
switch (day)
{
    case 1, 2, 3, 4, 5:
        print("평일입니다")
    default :
        print("주말입니다")    
}
//결과 : 평일입니다.
```
<br>

### where절
---
* where은 부가적으로 특정 패턴과 결합하여 조건을 추가해주는 역할을 한다.  
ex) switch문에서의 where사용
```swift
var year = 7
switch (year){
  case 0...9 where year == 1 || year == 6:
    print("월요일에 구매가 가능합니다.")
  case 0...9 where year == 2 || year == 7:
    print("화요일에 구매가 가능합니다.") 
  case 0...9 where year == 3 || year == 8:
    print("수요일에 구매가 가능합니다.") 
  case 0...9 where year == 4 || year == 9:
    print("월요일에 구매가 가능합니다.")  
  case 0...9 where year == 5 || year == 0:
    print("금요일에 구매가 가능합니다.")    
  default : 
    print("다시 입력해 주세요")
}
```

<br><br>

*출처)[Smile Han Swift 3주차](https://www.youtube.com/watch?v=eYKWGiTNibw&list=PLJqaIeuL7nuEEROQDRcy4XxC9gU6SYYXb&index=20)*




















