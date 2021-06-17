---
layout : post
title : "Winform_SplashScreen"
featured-img: JSP-study
categories : [Cpp]
---

# Winform Splash Screen
---
지난번에 구현했던 소스를 회사 프로그램에 다시 구현하려니 이미지가 안나오는 오류가 생겼었다.  
Thread를 사용해도 소스 순서대로는 나오지만 이미지가 나오지 않는 이유를 찾지 못했었는데, 박사님께서 새로운 아이디어를 내 주셨다. 결과는 완벽했다!  

## Timer & Task
---
기존에 구성했던 소스는 `await`를 이용해 `Task.Delay`를 했는데 Timer로 시간을 정해 정해진 시간이 지나면 이벤트 핸들러가 작동하는 방법이었다.  
아래는 SplashScreen의 소스 일부분이다.  
```csharp
public SplashScreen()
{
    InitializeComponent();
    timer1.Tick += (s, a) => this.Close();
}
 public SplashScreen(Image img)  : this()   //생성자 chain
{
    SetImageAndResizeForm(img);
}
public Task ShowSplashScreen(int loadTime) 
{
    return Task.Run(() => 
    {
        timer1.Interval = loadTime;
        timer1.Start();
        this.ShowDialog();
    });
}
```
함수 사용법은 전과 동일하지만 함수 안의 구성요소가 다르다.  
1. using System안에 있는 타이머를 사용한다.
2. 생성자에 타이머 이벤트 핸들러를 넣어준다.  
Tick은 `EventTimer Handler` 형으로 (object s, Eventargs a)형의 `람다식`으로 넣어준다.  
![/assets/img/posting/Winform_SplashScreen/Untitled.png](/assets/img/posting/Winform_SplashScreen/SplashScreen.png)
this.close()는 이벤트핸들러 형식이 아니기 때문에 람다식 함수 안에 넣어준다.  
3. ShowSplashScreen은 Task비동기 형식을 반환하는데 return Task.Run()으로 반환하자마자 시작한다.  
4. `timer1.Interval = loadTime`은 매개변수 loadTime으로 받은 ms초만큼 시간을 지정한다.  
5. `timer1.Start()`는 타이머를 시작시키는 함수이다.    
2500ms이면 2.5초를 세기 시작하고 시간이 되면 `timer1.Tick`에 등록한 이벤트 핸들러를 실행시킨다.
6. 비동기 형식으로 Program.cs에 인스턴스를 만들고 실행하면 비동기 형식으로 진행된다.  
아래 소스는 Program.cs의 소스 일부분이다.  

```csharp
SplashScreen screen = new SplashScreen(@".\Resources\SplashScreen_Finelocalizer.png");
Task splashScreen = screen.ShowSplashScreen(2500);
///비동기로 실행시킬 소스
FineLocalizerForm f = new FineLocalizerForm();
splashScreen.Wait(); //Task screen이 끝날때까지 기다림.
Application.Run(f); //실행
```

