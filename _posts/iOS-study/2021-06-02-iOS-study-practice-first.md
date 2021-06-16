---
layout : post
title : "iOS 간단한 실습"
featured-img: ios-study
categories : [iOS]
---

# ios 간단한 실습

Table View Add New Constraints 로 Table View화면 전체를 채움

![image1]({{"/assets/img/posting/2021-06-02-iOS-study-practice-first/Untitled.png"| relative_url}})

Assistant(ctrl+command+alt+enter)로 Table View의 outlet을 만들기

![Untitled1.png]({{"/assets/img/posting/2021-06-02-iOS-study-practice-first/Untitled1.png"| relative_url}})

UITableViewDataSource프로토콜을 채택시 오류가 나는 이유?

→UITableViewDelegate같은 경우 프로토콜 채택시 필수로 구연해야하는 메소드가 없기 때문에 오류가 나지 않지만 UITalbeViewDataSource의 경우 필수로 구현해야하는 요소가 있기 때문이다.

→Fix로 필수 메소드를 자동으로 만든다.

![Untitled2.png]({{"/assets/img/posting/2021-06-02-iOS-study-practice-first/Untitled2.png"| relative_url}})

![Untitled3.png]({{"/assets/img/posting/2021-06-02-iOS-study-practice-first/Untitled3.png"| relative_url}})

TableViewDataSource채택시 구현해야하는 메소드들 Required를 사용했기 때문에 반드시 구현이 필요하다

출처 : [https://developer.apple.com/documentation/uikit/uitableviewdatasource](https://developer.apple.com/documentation/uikit/uitableviewdatasource)

![Untitled4.png]({{"/assets/img/posting/2021-06-02-iOS-study-practice-first/Untitled4.png"| relative_url}})

적용된 모습

```swift
func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return 5
    }

func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        return UITableViewCell()
    }
```

viewDidLoad()메소드 안에 table.dataSource = self, table.delegate = self를 적어야만 cell의 textLabel이 보인다.

![Untitled5.png]({{"/assets/img/posting/2021-06-02-iOS-study-practice-first/Untitled5.png"| relative_url}})

section수 정하기

기본적으로 section은 1개로 지정되어있어 적어줄 필요는 없지만(optional)만약 세션이 한개 이상 필요하다면 numberOfSections메소드를 구현해 줘야 한다.

```swift
func numberOfSections(in tableView: UITableView) -> Int {
        return 3
    }
```

style을 .default 가 아닌 .subtitle을 적용하고 ,section수를 3개로 지정했을 경우

→ 기본적인 설정 외 다른 형식이 필요하다면 tableView Cell을 추가해서 구현하면 된다.

!["/assets/img/posting/2021-06-02-iOS-study-practice-first/Untitled6.png]({{"/assets/img/posting/2021-06-02-iOS-study-practice-first/Untitled6.png"| relative_url}})

!["/assets/img/posting/2021-06-02-iOS-study-practice-first/Untitled7.png]({{"/assets/img/posting/2021-06-02-iOS-study-practice-first/Untitled7.png"| relative_url}})

!["/assets/img/posting/2021-06-02-iOS-study-practice-first/Untitled8.png]({{"/assets/img/posting/2021-06-02-iOS-study-practice-first/Untitled8.png"| relative_url}})

  tableView에 이미지 추가하기

Assets.xcassets에 이미지를 추가한다

!["/assets/img/posting/2021-06-02-iOS-study-practice-first/Untitled9.png]({{"/assets/img/posting/2021-06-02-iOS-study-practice-first/Untitled9.png"| relative_url}})

출처 : flaticon.com

!["/assets/img/posting/2021-06-02-iOS-study-practice-first/Untitled10.png]({{"/assets/img/posting/2021-06-02-iOS-study-practice-first/Untitled10.png"| relative_url}})

table View Cell 사용 방법?.

아래처럼 설정을 해준다. 

!["/assets/img/posting/2021-06-02-iOS-study-practice-first/Untitled11.png]({{"/assets/img/posting/2021-06-02-iOS-study-practice-first/Untitled11.png"| relative_url}})

cocoa touch file로 custom할 cell의 클래스를 만들어준다.

!["/assets/img/posting/2021-06-02-iOS-study-practice-first/Untitled12.png]({{"/assets/img/posting/2021-06-02-iOS-study-practice-first/Untitled12.png"| relative_url}})

오브젝트들을 끌어서 cell안에 넣어준다.

!["/assets/img/posting/2021-06-02-iOS-study-practice-first/Untitled13.png]({{"/assets/img/posting/2021-06-02-iOS-study-practice-first/Untitled13.png"| relative_url}})

label을 MyTableViewCell에 connect해준다

!["/assets/img/posting/2021-06-02-iOS-study-practice-first/Untitled14.png]({{"/assets/img/posting/2021-06-02-iOS-study-practice-first/Untitled14.png"| relative_url}})

ViewController의 tableView코드를 수정해준다

dequeueReusableCell은 TableViewCell형식이지만 우리가 사용하고 싶은 label이 있는 클래스는 MyTableViewCell이므로 as!로 downCasting해준다.

!["/assets/img/posting/2021-06-02-iOS-study-practice-first/Untitled15.png]({{"/assets/img/posting/2021-06-02-iOS-study-practice-first/Untitled15.png"| relative_url}})