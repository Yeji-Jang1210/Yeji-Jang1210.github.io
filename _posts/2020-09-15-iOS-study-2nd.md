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

**Optional(옵셔널)/Optional Type 이란?**  
* Swift언어에 있는 새로운 개념으로, 자료형의 값을 저장하거나 **`nil`**을 저장 할 수 있다.  
    * **`nil`** : 값이 없는 것 
    * nil은 기본 자료형에서 저장할 수 없기 때문에 옵셔널 타입으로 선언해야한다.   
* 옵셔널 자료형 선언 방법
    * 자료형 뒤에 [?]나[!]를 붙여준다. 
    ex)
    ```swift
    var myNum : Int?  //옵셔널 정수형 myNum변수 선언  


    myNum = 8
    print(myNum)
    //결과 : Optional(8)
    ```  
    myNum의 자료형을 옵셔널타입으로 지정했기 때문에 결과는 8이 아닌 Optional(8)이 나오는 것이다.  
    Optional()이 나오는 것이 싫다면 아래와 같이 옵셔널을 풀어주면 된다.  
    ```swift
    print(myNum!)  //결과 : 8
    ```
<br>




