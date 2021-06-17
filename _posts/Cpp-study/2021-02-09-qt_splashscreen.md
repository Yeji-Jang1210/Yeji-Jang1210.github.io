---
layout : post
title : "WinForm_SplashScreen"
featured-img: JSP-study
categories : [Cpp]
---

# Winform과 C#을 활용한 SplashScreen구현
---

## Qt?
---
Qt는 Linux, Windows, macOS, Android 또는 임베디드와 같은 다양한 소프트웨어 및 하드웨어 플랫폼에서 실행되는 `크로스 플랫폼 애플리케이션`뿐만 아니라 그래픽 사용자 인터페이스를 생성하기위한 위젯 툴킷이라고 위키백과에 나와있다.  
출처)[Qt](https://en.wikipedia.org/wiki/Qt_(software))  

## 비동기식 splash screen 구현
---
### 비동기
---
**비동기 프로그램**  
<u>사용 이유?</u>  
컴퓨터는 다음 명령문으로 이동하기 전에 작업이 완료될 때까지 컴퓨터는 각 명령문에서 차단된다.  
따라서 작업이 완료될때까지 다음 작업을 기다리는데 기다리는 동안 아무것도 하지 않아 시간이 효율적이지 못함.  
<br>  

**비동기와 병렬의 차이점**  
병렬 : 하나의 작업을 여러 작업자가 나눠 수행 뒤 하나의 결과로 만드는 것  
비동기 : 하나의 작업의 결과가 나올 때 까지 대기하는 대신 곧이어 다른 작업을 수행하고 먼저 수행하던 작업의 이 끝난다면 그 때 결과를 받아내는 처리  

**비동기식 프로그램 작성 방법**  
1.	await 연산자 사용 : 
    * await 연산자는 비동기 작업이 완료될 때 까지 바깥쪽 비동기 메서드의 평가를 일시 중단, 완료 시 await연산자는 작업 결과를 반환(return 값 有 경우)  
    * await 연산자는 스레드를 차단하지 않음  
    * 값을 생성하지 않는 비동기 작업의 경우 Task.Wait 호출이 가능  
2.	Task  
    * Task.Start() : Task 인스턴스가 Task를 생성할 때 넘겨받은 Action을 비동기로 실행  
    * Task.Run() : Task 인스턴스를 만든 후 실행까지 한 번에 할 수 있는 메서드  
Ex) Task.Start()와 Task.Run 의 차이  

```csharp
Action someAction = () => 
{
Thread.Sleep(1000);
Console.WriteLine(“Printed asynchronously”);
};
Task myTask = new Task(someAction);
myTask.Start();
Console.WriteLine(“Printed synchronously”);
myTask.Wait();
```

```csharp
Task myTask = Task.Run( () =>
{
Thread.Sleep(1000);
Console.WriteLine(“Printed asynchrounously”);
});
Console.WriteLine(“Printed synchronously”);
myTask.Wait();
```
<br>

* Action 대리자는 Thread.Sleep(1000); 때문에 최소 1초는 소요 그전에 프로그램이 “Printed synchronously”를 출력 후 myTask.Wait()메소드 호출부로 가 myTask가 실행 중인 비동기 코드가 완료될 때까지 대기한다.  
someAction 대기자가 “Printed asynchronously”를 출력하고 종료한다.  
 
* Task.Delay() : 해당 스레드에 흐름 넘기고 논리적으로 시간을 기다리는 메서드로 Thread.Sleep()의 비동기 버전이라 생각하면 쉽다.  
두개의 차이점은 Thread.Sleep의 경우 스레드를 블록(차단)시킴  
: Task.Delay()를 사용하면 해당 메소드의 반환 여부와 관계없이  UI가 사용자에게 잘 응답함.  
* Task.Wait() : 호출한 스레드 작업이 완료 될 때까지 대기  
<br>

3.	async 한정자 사용  
    * async 한정자는 코드를 만날 때 까지 호출 결과를 기다리지 않고 다음 코드로 이동하도록 실행코드 생성함  
    * async으로 정의된 메소드는 반환형이 void거나 Task<Result>형 이어야 함  
    * void 형일 경우 await연산자가 없어도 비동기식으로 진행  
    * Task<Result>형일 경우 함수 내부의 await연산자를 찾아 그곳에서 호출자에게 제어를 돌려주도록 실행 파일 만든다(찾지 못하는 경우 동기식으로 진행)  
<br>

4.	명명 규칙  
    * 반환형 있는 비동기 메소드 이름 : 접미사로 “Async”을 붙임  
    * 반환형 없는 비동기 메소드 이름 : 접두사로 “Begin”, “Start”붙임  

<br>
<br>

### 소스코드
---
1. Winform  
비동기로 실행되는 SplashScreen  

SplashScreen.cs : [https://github.com/yejiJang-COGAPLEX/testSource_Csharp/blob/master/testSplashScreen/testSplashScreen/SplashScreen.cs](https://github.com/yejiJang-COGAPLEX/testSource_Csharp/blob/master/testSplashScreen/testSplashScreen/SplashScreen.cs)

- Resource에 저장한 사진을 찾아 사진의 크기에 맞게 띄움  
- 지정한 사진이 디렉토리에 위치하지 않을경우 흰색 바탕으로 실행 됨  
- SplashScreen의 생성자로 String imageName이나 Image image로 사진을 찾음  

Main1 : [https://github.com/yejiJang-COGAPLEX/testSource_Csharp/blob/master/testSplashScreen/testSplashScreen/Main1.cs](https://github.com/yejiJang-COGAPLEX/testSource_Csharp/blob/master/testSplashScreen/testSplashScreen/Main1.cs)  

- #DEFINE으로 배포모드와 개발모드를 지정할 수 있음  
<br>

2. QT  

```cpp
int main(int argc, char *argv[])
{
    QApplication a(argc, argv);
    QApplication::setStyle(QStyleFactory::create("Fusion"));
    // QApplication::setAttribute(Qt::AA_DisableWindowContextHelpButton);
#ifdef DISTRI   
    QSplashScreen* screen = new QSplashScreen();
    std::future<void> f1 = loadSplashScreen(screen,3, ":/splash/splash/splash_window.png");

    copick3d::CmdLine::Print("MainWindow load..");
#endif
    MainWindow* w = nullptr;
    if (argc == 3)
    {
        w = new MainWindow(argv[1], argv[2]);
    }
    else
    {
        w = new MainWindow();
    }
    copick3d::CmdLine::Print("Main Window complete");
#ifdef DISTRI
    f1.wait();
    screen->close();
    copick3d::CmdLine::Print("splash screen closed and Show MainWindow");
#endif
    w->show();
    return a.exec();
}
std::future<void> loadSplashScreen(QSplashScreen* screen,int seconds, const QString &filePath) //return type future
{
    QPixmap* img = new QPixmap(filePath);
    screen->setPixmap(*img);
    copick3d::CmdLine::Print("show splash screen");
    screen->show();
    return std::async(std::launch::async, [seconds, screen]
    {
        sleep_for(std::chrono::seconds(seconds));
    });
}
```

비동기식으로 실행되는 Splash Screen

- 기존의 구현했던 것은 SplashImage가 실행될 때 MainWindow를 load하지 않았음
- 배포모드일때만 SPlashScreen의 실행 추가
- screen→close()를 함수 안으로 옮길 수 있는 방법 필요
- splashscreen 클래스 : [https://doc.qt.io/qt-5/qsplashscreen.html](https://doc.qt.io/qt-5/qsplashscreen.html)
- QPixmap의 이미지 경로는 resource.qrc에 :/splash/splash에 위치하는 splash.png(test용)입니다.
→변경할 이미지 필요

- [x]  개발 중에는 스플래시 이미지 뜨지 않게 설정 가능하도록 #define 응용해보기