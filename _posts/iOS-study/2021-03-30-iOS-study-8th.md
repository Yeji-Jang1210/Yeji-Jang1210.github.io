---
layout : post
title : "iOS공부 : 08주차"
featured-img: ios-study
categories : [iOS]
---
# 프로토콜의 활용
---
프로토콜이 어떻게 사용되는지 이해하기 위해 실제로 사용하는 UITableView 클래스와 예제를 살펴보면서 정리하였다.  
<br>

# 프로토콜을 채택하여 사용하는 UITableView
---
UITableView는 클래스 혼자 동작하기엔 어려움으로 프로토콜을 채택하여(adopt) 사용하는데 이를 정상적으로 사용하기 위해서는 DateSource와 Delegate 프로토콜을 채택하여 사용한다.  
`DateSource` : 데이터 모델(MVC:Model,View,Controll)중 M에 해당한다.  
`Delegate` : Delegate는 대리자의 역할로 하나의 객체가 모든 일을 처리하는 것이 아닌 일의 일부를 다른 객체에 넘기는 역할을 한다.  (swift언어 말고도 c#등 다른언어에도 Delegate가 존재한다.)  
<br>

## TableView의 DataSource : UITableViewDataSource프로토콜
---
### 1. func tableView(_:numberOfRowsInSection:)
---

```swift
override func tableView(_ tableView: UITableView, numberOfRowsInSection section : Int)->Int
{
	return items.count	
}

```

* 함수 기능 : 테이블뷰의 지정된 섹션에 있는 행(TableViewCell) 수를 반환하도록 데이터 소스에 지시한다.  
* TableView에서 UITableViewDataSource프로토콜을 채택하여 사용하기 때문에 프로토콜에 선언되어있는 함수를 override하여 사용자가 정의한다.   
* 이 함수는 `Required`로 <u>프로토콜로 채택하면 반드시 구현해야하는 함수</u>이다.  
* 함수는 Int형을 반환하고 _(tableView)는 UITableView형, numberOfRowInSection은 Int형인 매개변수이다.  위의 함수에서는 item의 개수를 정수형으로 반환한다.   
* 예제  
```swift
let items: [String] = ["A", "B", "C"]
func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int 
{
      return items.count	//4
}
``` 

-> 섹션의 셀의 수(행의 개수)를 items배열의 크기만큼 반환한다.  

출처)[UITableViewDataSource](https://developer.apple.com/documentation/uikit/uitableviewdatasource)
<br>

### 2. func tableView(_:cellForRowAt:)
---
```swift
override func tableView(_ tableView: UITableView, cellForRowAt indexPath : IndexPath)-> UITableViewCell 
{
    let cell = tableView.dequeueReusableCell(withIdentifier : “cellTypeIdentifier”, for：indexPath)
	cell.textLabel!.text = “Cell text”
	return cell
}
```
* 함수 기능 :　테이블 뷰의 특정위치에 있는 셀의 데이터 소스를 요청한다.  
* UITableViewDataProtocol을 채택하여 사용해 다른 클래스를 구현할 때 함수를 override한다.  
* 반환형이 UITableViewCell이고 Required로 되어있기 때문에 프로토콜 채택 후 반드시 구현해야하는 함수이다.  
* tableView.dequeueReusableCell(withIdentifier:for:) 은 지정된 재사용 식별자에 대해 재사용 가능한 테이블 뷰 셀 객체를 반환하고 테이블에 추가한다.  return : UITableViewCell
	* widthIdentifier : 재사용할 객체의 식별자를 문자열로 받는다. nil이 매개변수면 안된다.  
	* for : IndexPath를 사용하여 테이블 보기에서 셀의 위치를 ​​기반으로 추가 구성을 수행한다.   
* cell.textLabel!.text = “Cell text” textLabel은 옵셔널 형으로 되어있기 때문에 강제언래핑 해준다.  (text는 string형이기때문)
* return cell UITableViewCell형인 cell을 반환한다.  
* 예제
```swift
override func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
    let cell = tableView.dequeueReusableCell(withIdentifier: "reuseIdentifier", for: indexPath)
    cell.textLabel?.text = items[indexPath.row]
    return cell
}
```

-> indexPath이고 재사용 가능한 식별자가 reuseIdentifier-인 셀을 반환해 셀의 이름을 items의 배열에 indexPath.row에 해당하는 값을 cell의 텍스트로 지정해주고 셀을 반환한다.  

예제 출처)[TableViewController사용법](https://zeddios.tistory.com/54)

<br>

## TableView의 Delegate : UITableViewDeleate프로토콜
---
TableView의 Delegate에는 여러 함수가 존재하지만 그중에 두개만 살펴보았다.  

### optional func tableView(_:didSelectRowAt:)
---
```swift
optional func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath)
{
	print(“\(items[indexPath.row]) is selected”)
}
```
->테이블 뷰의 새로운 행이 선택되었을 때 indexPath의 행에 해당하는 item값을 프린트한다.(console)  
* 함수 기능 : 행이 선택됐다는 것을 델리게이트에게 전달하는 기능  
* return형이 void이고 `optional` func형이기 때문에 <u>프로토콜을 채택하여도 이 함수는 구현하지 않아도 된다.</u>  
* tableView : 새로운 행이 선택되었을 때 알려줄 tableView  
* indexPath : 테이블 뷰의 새로운 행이 선택되었을때의 위치의 인덱스경로  

<br>

### optional func tableView(_:didDeselectRowAt:)
---
```swift
optional func tableView(_ tableView: UITableView, didDeselectRowAt indexPath: IndexPath)
{
	print(“\(items[indexPath.row] is deselected”)
}
```
* 함수 기능 : 지정된 행의 선택이 취소되었다는 것을 델리게이트에게 전달하는 기능  
* return형이 void이고 optional func형이기 때문에 프로토콜을 채택하여도 이 함수는 구현하지 않아도 된다.  
* tableView : 새로운 행이 선택되었을 때 알려줄 tableView  
* indexPath : 테이블 뷰의 새로운 행이 선택되었을때의 위치의 인덱스경로  

출처)[UITableViewController](https://developer.apple.com/documentation/uikit/uitableviewdelegate)

## UITableView Delegate, DataSource 그림
---
UITableView가 동작하는 방법을 그림으로 그려보았다.  
프로토콜을 여러개 채택하여 클래스를 구현할 경우 클래스 안이 복잡해지고 가독성이 떨어지기 때문에 swift에서는 프로토콜을 여러개 채택하여 사용할때는 구분하기 쉽도록 `extension`을 사용한다.  

![UITableView]({{"/assets/img/posting/Study_iOS_img/UITableView_img.png"| relative_url}})