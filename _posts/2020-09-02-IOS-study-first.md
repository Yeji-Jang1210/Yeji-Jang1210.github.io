---
layout : post
title : "iOS공부 : 01주차"
featured-img: ios-study
---
# 1주차 OT
---
<br>
01주차 과제 : 
아래의 그림과 같은 결과가 나오게 소스를 작성하세요.  
![Image Alt ios_결과]({{"/assets/img/posting/Study_iOS_img/Study_iOS_post1/iOS_결과.png"| relative_url}})  

* 실행 홈페이지 : [Repl.it](https://repl.it/languages/swift)  
    처음 들어가면 다음과 같은 화면이 나온다.  
    ![Image Alt Swift_ot]({{"/assets/img/posting/Study_iOS_img/Study_iOS_post1/Swift_ot.png"| relative_url}})  

    <br>
    <br>
    <br>

* 소스 작성창에 [examples]를 누르면 예시 소스를 볼 수 있는데,  
    [반복할 숫자] : [홍길동] 을 작성해야 하므로 `for 반복문`을 사용해야한다.  
    ![Image Alt Swift_ot2]({{"/assets/img/posting/Study_iOS_img/Study_iOS_post1/Swift_ot2.png"| relative_url}})  

    <br>
* 클릭하면 예시 소스가 소스 작성창에 작성된다.  
    ![Image Alt Swift_ot3]({{"/assets/img/posting/Study_iOS_img/Study_iOS_post1/Swift_ot3.png"| relative_url}})  

    아직 Swoft언어를 배우지 않았지만 for반복문 구조만 살펴보면,  

    <b>for문 구조 </b>
    ```Swift
        for i in 1...10 {       
            print("Number: \(i)")            
        }                               
    ```
    ```
    for [임시변수] in `범위`{              
       반복할 문장  
        }  
    ```    

    **`범위`**
    : A...B    → A,B를 포함한 A부터 B까지의 범위  
    : A..< B   → A를 포함하고 B를 포함하지 않은 A부터 B까지의 범위  

    <br>
    우리는 반복할 숫자가 앞에 있으므로 print 문을 <u>print("/(i) : 홍길동") </u>로 바꿔준다.  
    (Swift언어는 세미콜론이 필요 없나보다.)  

* 결과:  
    ![Image Alt ios과제_결과]({{"/assets/img/posting/Study_iOS_img/Study_iOS_post1/ios_1주차_과제.png"| relative_url}})    



