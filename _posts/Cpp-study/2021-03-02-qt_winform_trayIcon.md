---
layout : post
title : "Qt_WinForm TrayIcon"
featured-img: JSP-study
categories : [Cpp]
---
# **1. QT**

mainWindow.h와 mainWindow.cpp에 추가

- **mainWindow.h**

```csharp
public slots:
    void createTrayIconMenu();
    void trayIconDoubleClick(QSystemTrayIcon::ActivationReason reson);

private:
    Ui::mainWindowClass ui;
    QSystemTrayIcon *windowTrayIcon;

    QMenu *trayIconMenu;
    QMenu *mainMenu;

    QAction *viewMainWindow;
    QAction *closeMainWindow;
    QAction *subMenu;
```

1. createTrayIconMenu(); - trayIcon에 연결되는 메뉴바 생성
2. trayIconDoubleClick(QSystemTrayIcon::ActivationReson reson); - trayIcon을 더블클릭 했을 때의 최소화 main창 열기
3. QAction *viewMainWindow, QAction *closeMainWindow - 시그널이 발생할 Action
- **mainWindow.cpp**

```csharp
mainWindow::mainWindow(QWidget *parent)
    : QMainWindow(parent)
{
    ui.setupUi(this);
    QIcon icon(":/mainWindow/icons/icon.png");
    windowTrayIcon = new QSystemTrayIcon(icon,this);
    //windowTrayIcon = new QSYstemTrayIcon(this);
    //windowTrayIcon->setIcon(icon);
    windowTrayIcon->setVisible(true);
    windowTrayIcon->setToolTip("Tray Program");
    windowTrayIcon->showMessage("title","comments",icon,1000);  //balloon Message
    
    createTrayIconMenu();
    connect(windowTrayIcon,SIGNAL(activated(QSystemTrayIcon::ActivationReason)),this,SLOT(trayIconDoubleClick(QSystemTrayIcon::ActivationReason)));
		//더블클릭하는 signal이 windowTrayIcon에서 발생하면 mainWindow클래스의 trayIconDoubleClick함수에 signal결과를 보냄
    windowTrayIcon->setContextMenu(trayIconMenu);
    windowTrayIcon->show();   
}
```

setIcon(QIcon icon); - 아이콘을 설정

setContextMenu(trayIconMenu); - QMenu클래스형으로 만든 메뉴를 트레이 아이콘의 메뉴로 지정

![assets/img/posting/trayIcon_img/Untitled.png](assets/img/posting/trayIcon_img/Untitled.png)

setToolTip("Tray Program");

![assets/img/posting/trayIcon_img/Untitled1.png](assets/img/posting/trayIcon_img/Untitled1.png)

QSystemTrayIcon Signal을 발생

![assets/img/posting/trayIcon_img/Untitled2.png](assets/img/posting/trayIcon_img/Untitled2.png)

createTrayIconMenu();

![assets/img/posting/trayIcon_img/Untitled3.png](assets/img/posting/trayIcon_img/Untitled3.png)

showMessage(title, message,icon,msTimeoutHint);

- **mainWindow.cpp** - void mainWindow::createTrayIconMenu()

```csharp
void mainWindow::createTrayIconMenu() 
{
    trayIconMenu = new QMenu(this);
    viewMainWindow = new QAction("Open", this);
    closeMainWindow = new QAction("Exit", this);
		subMenu = new QAction("SubMenu", this);

		//메뉴에 만들어 놓은 액션 추가
    trayIconMenu->addAction(viewMainWindow);
		trayIconMenu->addSeparator(); //Open과 Exit사이 밑줄 추가
    trayIconMenu->addAction(closeMainWindow);
		
		mainMenu = trayIconMenu->addMenu("mainMenu");  //trayIconMenu에 mainMenu추가
    mainMenu->addAction(subMenu);  //mainMenu에 subMenu action추가

    connect(viewMainWindow, SIGNAL(triggered()), this, SLOT(showNormal()));
    connect(closeMainWindow, SIGNAL(triggered()), this, SLOT(close()));
}
```

![assets/img/posting/trayIcon_img/Untitled4.png](assets/img/posting/trayIcon_img/Untitled4.png)

QWidget의 Slots

![assets/img/posting/trayIcon_img/Untitled5.png](assets/img/posting/trayIcon_img/Untitled5.png)

QAction의 Signal

- **mainWindow.cpp** - void mainWindow::trayIconDoubleClick(QSystemTrayIcon::ActivationReson)

```csharp
void mainWindow::trayIconDoubleClick(QSystemTrayIcon::ActivationReason reson)
{
    if (reson == QSystemTrayIcon::DoubleClick) 
    {
        if (this->isMinimized()) 
        {
            this->showNormal();
        }
        else 
        {
            this->showMinimized();
        }
    }
}
```

mainWindow에서 Signal이 발생했을때 받는  SLOT의 함수

보낸 시그널이 DoubleClick일 경우 실행

1. 화면이 최소화 이면 : 다시 원상태로 띄움
2. 화면이 원상태 이면 : 최소화 함

출처) QT QAction Class :  [https://doc.qt.io/qt-5/qaction.html](https://doc.qt.io/qt-5/qaction.html)

    QT QSystemTrayIcon : [https://doc.qt.io/qt-5/qsystemtrayicon.html](https://doc.qt.io/qt-5/qsystemtrayicon.html)

    QT QMenu : [https://doc.qt.io/qt-5/qmenu.html#separatorsCollapsible-prop](https://doc.qt.io/qt-5/qmenu.html#separatorsCollapsible-prop)

    TrayIcon 구현 예제 : [http://www.qt-dev.com/board.php?board=lecboard&category=3&command=body&no=77](http://www.qt-dev.com/board.php?board=lecboard&category=3&command=body&no=77)

※ 기존에 test로 만든 splash screen과 합쳐봤을 때 이상x

# **2. WinForm**

1. notifyIcon (상속 불가)

![assets/img/posting/trayIcon_img/Untitled6.png](assets/img/posting/trayIcon_img/Untitled6.png)

- 사용시 Visible =  true로 설정 (this.notifyIcon.Visigle = true;)
- ContextmenuStrip : 트레이 아이콘의 메뉴를 사용가능
    - [도구상자]-[contextMenuStrip]사용해 notifyIcon과 연결
- Icon : ico확장자 파일만 사용 가능 (this.notifyIcon1.Icon = new Icon("iconName.ico");
- link : [https://docs.microsoft.com/ko-kr/dotnet/api/system.windows.forms.notifyicon?view=net-5.0](https://docs.microsoft.com/ko-kr/dotnet/api/system.windows.forms.notifyicon?view=net-5.0)

2. ContextMenuStrip

![assets/img/posting/trayIcon_img/Untitled7.png](assets/img/posting/trayIcon_img/Untitled7.png)

![assets/img/posting/trayIcon_img/Untitled8.png](assets/img/posting/trayIcon_img/Untitled8.png)

- notifyIcon 오른쪽 마우스 눌렀을 때 나타나는 메뉴
- [도구상자]-[contextMenuStrip]으로 드래그 후 추가

3. 기능
3.1. notifyIcon Double Click

```csharp
private void notifyIcon1_MouseDoubleClick(object sender, MouseEventArgs e)
{
    if(this.WindowState == FormWindowState.Minimized)
    {
        this.WindowState = FormWindowState.Normal;
    }
    else
    {
        this.WindowState = FormWindowState.Minimized;
    }
    this.Activate();
}
```

WindowState를 사용해 최소화일때는 원래 크기로 띄우고 아닐경우는 최소화하는 기능

3.2. contextMenuStrip으로 Form open

```csharp
private void mainFormToolStripMenuItem_Click(object sender, EventArgs e)
{
    if (this.WindowState == FormWindowState.Minimized)
    {
        this.WindowState = FormWindowState.Normal;
    }
    this.Activate();
}
```

3.3. 다른 Form open

```csharp
private void form2ToolStripMenuItem_Click(object sender, EventArgs e)
{
    foreach (Form openForm in Application.OpenForms)
    {
        if (openForm.Name == "Form2")
        {
            if (openForm.WindowState == FormWindowState.Minimized)
            {
                openForm.WindowState = FormWindowState.Normal;
                openForm.Owner = this;
            }
            openForm.Activate();
            return;
        }
    }
    Form2 form2 = new Form2();
    form2.Location = new Point(this.Location.X + this.Size.Width, this.Location.Y);
    form2.Show();
}
```

Application.OpenForms로 Form이 열려있는지 확인 아닐경우 새 폼을 Open

form2.Location의 위치는 메인 폼의 옆에 위치한다.

3.4. balloonTip

![assets/img/posting/trayIcon_img/Untitled9.png](assets/img/posting/trayIcon_img/Untitled9.png)

notifyIcon에 알림기능을 추가 balloonTip의 알림이 사라질때 아래 작업표시줄의 notifyIcon도 함께 사라짐

```csharp
//ShowBalloonTip 사용법
notifyIcon.ShowBalloonTip (int timeout, string tipTitle, string tipText, System.Windows.Forms.ToolTipIcon tipIcon);
//ToolTipIcon종류 열거형으로 정의되어있음
//ToolTipIcon.None : 표준 아이콘 없음 (0)
//ToolTipIcon.Info : 정보 아이콘 (1)
//ToolTipIcon.Warring : 경고 아이콘 (2)
//ToolTipIcon.Error : 에러 아이콘 (3)
```

3.5. exit

```csharp
private void exitToolStripMenuItem_Click(object sender, EventArgs e)
{
    notifyIcon.Visible = false;
    notifyIcon.Dispose();
    Application.Exit();
}
```

4. 다른 Form에서의 NotifyIcon 사용

4.1. MainForm에 notifyIcon 프로퍼티를 static으로 선언

```csharp
public static NotifyIcon Notifier 
{ 
   get
   { 
      return notifyIcon; 
   } 
}
private static NotifyIcon notifyIcon;
```

4.2. main1함수 안에 만들어둔 notifyIcon1 대입

```csharp
public Main1()
{
	InitializeComponent();
	notifyIcon = this.notifyIcon1;
}
```

4.3. 다른 Form에서의 사용 ( Notifier이 get으로 notifyIcon을 반환하기 때문에 사용 가능)

```csharp
Main1.Notifier.ShowBalloonTip(1000,"hello", "this is Form2",ToolTipIcon.Info);
```

![assets/img/posting/trayIcon_img/Untitled10.png](assets/img/posting/trayIcon_img/Untitled10.png)