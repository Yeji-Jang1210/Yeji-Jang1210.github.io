---
layout : post
title : "JSON을 사용한 영화 정보 앱 만들기"
featured-img: ios-study
categories : [iOS]
---

# JSON을 사용한 영화 정보 앱 만들기

# UI - Main.storyboard

---

전체적인 ui storyboard모습

![Untitled]({{"/assets/img/posting/Study_iOS_img/2021-06-17-iOS-study-practice-4th/Untitled.png" | relative_url}})

# Active Screen

---

각 기능을 실행했을 때 나오는 스크린

- viewController에서 각 셀을 눌렀을 경우 naver에서 영화를 검색한다.
- theater 탭 컨트롤 터치 시 네이버 map에서 영화관을 검색한다.
- cinema 탭 컨트롤 터치 시 각 영화관 버튼이 나오고 버튼 클릭시 모바일 웹 페이지로 이동한다.

![Untitled1]({{"/assets/img/posting/Study_iOS_img/2021-06-17-iOS-study-practice-4th/Untitled1.png" | relative_url}})

# 영화 진흥 위원회 API

---

영화 진흥 위원회는 영화 정보와 박스 오피스 API를 제공하고 있다.

위 앱에서는 일별 박스오피스를 사용했지만 그 외에 목록과 상세정보 API도 제공하고 있다.

![Untitled2]({{"/assets/img/posting/Study_iOS_img/2021-06-17-iOS-study-practice-4th/Untitled2.png" | relative_url}})

제공 서비스에 들어가면 REST와 SOAP방식별 기본 요청 URL과 parameter사용법이 나와있다.

![Untitled3]({{"/assets/img/posting/Study_iOS_img/2021-06-17-iOS-study-practice-4th/Untitled3.png" | relative_url}})

아래는 영화진흥위원회 API 서비스 이용안내이다.

![Untitled4]({{"/assets/img/posting/Study_iOS_img/2021-06-17-iOS-study-practice-4th/Untitled4.png" | relative_url}})

# 주요기술 및 추가한 소스

---

![Untitled5]({{"/assets/img/posting/Study_iOS_img/2021-06-17-iOS-study-practice-4th/Untitled5.png" | relative_url}})

![Untitled6]({{"/assets/img/posting/Study_iOS_img/2021-06-17-iOS-study-practice-4th/Untitled6.png" | relative_url}})

# 주요 소스코드

---

## viewController.swift

```swift
//
//  ViewController.swift
//  MovieJYJ
//
//  Created by 소프트웨어컴퓨터 on 2021/05/24.
//
import UIKit
//json으로 가져온 데이터에 관련된 구조체들
struct MovieData : Codable{
    let boxOfficeResult : BoxOfficeResult
}
struct BoxOfficeResult : Codable{
    let dailyBoxOfficeList : [DailyBoxOfficeList]
}
struct DailyBoxOfficeList : Codable{
    let movieNm : String
    let audiCnt : String
    let rank : String
    let rankInten : String
}
class ViewController: UIViewController,UITableViewDelegate,UITableViewDataSource {
    @IBOutlet weak var table: UITableView!
    var movieData : MovieData?
	//영화진흥위원회의 API url입력
    var movieURL = "https://www.kobis.or.kr/kobisopenapi/webservice/rest/boxoffice/searchDailyBoxOfficeList.json?key=2be0eea1573fd8856398115845381a81&targetDt="//20210525
	//로드시 실행되는 함수 
    override func viewDidLoad() {
        super.viewDidLoad()
        table.delegate = self
        table.dataSource = self
		
		//로드시 API URL뒤에 날짜 추가
        movieURL += makeYesterdayString()
		//API 데이터 가져옴
        getData()
    }
    func makeYesterdayString() -> String
    {
		//전날 일자로 가져온다.
        let y = Calendar.current.date(byAdding: .day, value: -1, to: Date())!
        let dateF = DateFormatter()
		//데이터 포맷형식
        dateF.dateFormat = "yyyyMMdd"
		//string형식으로 변경
        let day = dateF.string(from: y)
        return day
    }
    func getData(){
        //1. URL 만들기
        if let url = URL(string:movieURL){
            //2. Session만들기
            let session = URLSession(configuration:.default)
            //3. URLSession 인스턴스에게 task주기
            let task = session.dataTask(with: url) { (data, response, error) in
                if error != nil{
                    print(error!)
                    return
                }
                if let JSONdata = data{ //data is Optional Type
                    //print(JSONdata)
                    let dataString = String(data:JSONdata,encoding: .utf8)
                    print(dataString!)
                    let decoder = JSONDecoder()
                    do{ //error handling
                        let decodeData = try decoder.decode(MovieData.self, from: JSONdata)  //.self : static metatype
                        self.movieData = decodeData //uses self. inside closure
						//DispatchQueue : 앱의 기본 스레드 및 백그라운드 스레드에서 작업 실행을 순차,동시처리로 관리하는 개체
                        DispatchQueue.main.async{	//async으로 비동기적 실행
                            self.table.reloadData()
                        }
                    }catch{
                        print(error)	//error출력
                    }
                }
            }
            //task 시작하기(task.resume())
            task.resume()
        }
    }
	//ViewController에게 segue가 수행될 예정임을 알리는 함수
    override func prepare(for segue: UIStoryboardSegue, sender: Any?) {
        /* let dest = segue.destination as! DetailViewController   //segue.destination을 DetailViewController형으로 캐스팅
    	dest.movieName = "영화이름" */	
		//destination프로퍼티는 segue가 목적지를 접근하는 컨트롤러임 ( as?로 다운캐스팅)
        guard let dest = segue.destination as? DetailViewController else{ return }
        //dest.movieName = "영화이름"
		//선택된 테이블의 인덱스
        let myIndexPath = table.indexPathForSelectedRow!
        let row = myIndexPath.row
		//dest는 DetailViewController이므로 movieName변수에 접근이 가능함
        dest.movieName = (movieData?.boxOfficeResult.dailyBoxOfficeList[row].movieNm)!
    }
    func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
		//영화진흥위원회에서 제공하는 데이터 (movieData)의 dailyBoxOfficeList의 개수를 반환
		//guard let으로 count 사용가능(false일 경우 중괄호 수행)
        guard let count = movieData?.boxOfficeResult.dailyBoxOfficeList.count else { return 0 }
		//반환형 : Int
        return count
    }
    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
		//다운캐스팅으로 custom tableView cell을 cell에 적용(강제언레핑)
        let cell = tableView.dequeueReusableCell(withIdentifier: "myCell", for: indexPath) as! MyTableViewCell
		//cell의 movieName라벨의 text의 값(dailyBoxOfficeList 구조체 프로퍼티) 대입
        cell.movieName.text = movieData?.boxOfficeResult.dailyBoxOfficeList[indexPath.row].movieNm
		//cell의 movieRank라벨의 text의 값(dailyBoxOfficeList 구조체 프로퍼티) 대입
        cell.movieRank.text = movieData?.boxOfficeResult.dailyBoxOfficeList[indexPath.row].rank
		//cell의 movierankIntecnt라벨의 text의 값(dailyBoxOfficeList 구조체 프로퍼티) 대입
        cell.rankIntencnt.text = movieData?.boxOfficeResult.dailyBoxOfficeList[indexPath.row].rankInten
        if let cnt = movieData?.boxOfficeResult.dailyBoxOfficeList[indexPath.row].audiCnt{
            let numF = NumberFormatter()
			//천단위 구분기호 적용
            numF.numberStyle = .decimal
			//Int로 형변환 후 강제 언래핑
            let aCount = Int(cnt)!
			//numberStyle을 aCount에 적용후 string으로 형변환, 뒤에 '명'까지 합해줌
            let result = numF.string(for:aCount)!+" 명"
            cell.movAudiCnt.text = "누적 관람객 수 : \(result)"
        }
		//1,2,3위에 라벨 배경색을 변경하는 함수(구현)
        rankColor(cell : cell)
		//순위가 올라갔는지 떨어졌는지 이미지 표시하는 함수(구현)
        loadRankInTenImg(cell : cell)
        return cell
    }
    func tableView(_ tableView : UITableView, heightForRowAt indexPath : IndexPath)->CGFloat{
		//cell의 높이를 고정해줌
        return 100
    }
    func numberOfSections(in tableView: UITableView) -> Int {
		//세션의 개수를 지정
        return 1
    }
    func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
        //print(indexPath.description)
    }
    func tableView(_ tableView : UITableView, titleForHeaderInSection section:Int)->String?{
     	//세션의 header에 들어갈 text 적용 - 박스오피스(영화진흥위원회제공:20210608)
		return "박스오피스(영화진흥위원회제공:"+makeYesterdayString()+")"
    }
    func rankColor(cell : MyTableViewCell){
        if let c = cell.movieRank.text
        {
			//string형 c를 Int로 형변환
            switch Int(c)
            {
				//1등
                case 1:
					//movieRank라벨의 backgroundColor의 색을 지정
                    cell.movieRank.backgroundColor = UIColor(red: 255/255, green: 84/255, blue: 69/255, alpha: 1.0)
                case 2:
                    cell.movieRank.backgroundColor = UIColor(red: 255/255, green: 168/255, blue: 69/255, alpha: 1.0)
                case 3:
                    cell.movieRank.backgroundColor = UIColor(red: 255/255, green: 224/255, blue: 69/255, alpha: 1.0)
                default:
                    cell.movieRank.backgroundColor = UIColor(red: 217/255, green: 217/255, blue: 217/255, alpha: 1.0)
            }
        }
    }
    func loadRankInTenImg(cell:MyTableViewCell){
        var imgName : String = ""
		//guard let을 이용한 옵셔널 언래핑
        guard let c = Int(cell.rankIntencnt.text!) else { return }
		//순위가 올랐을 경우
        if(c > 0){
            imgName = "up.png" | relative_url}}"
        }else if(c < 0){	//떨어졌을경우
            imgName = "down.png" | relative_url}}"
        }else{				//변동없음
            imgName = "zero.png" | relative_url}}"
        }
		//cell의 rankIntenimage의 image(?.로 옵셔널체이닝 사용)에 적용할 이미지 추가
        cell.rankIntenimg?.image = UIImage(named: imgName)
    }
}
```

## MyTableViewCell.swift

---

```swift
//
//  MyTableViewCell.swift
//  MovieJYJ
//
//  Created by 소프트웨어컴퓨터 on 2021/05/24.
//
import UIKit
class MyTableViewCell: UITableViewCell {
	//custom tableView cell의 컨트롤들
    @IBOutlet weak var rankIntencnt: UILabel!
    @IBOutlet weak var rankIntenimg: UIImageView!
    @IBOutlet weak var movieName: UILabel!
    @IBOutlet weak var movieRank: UILabel!
    @IBOutlet weak var movAudiCnt: UILabel!
    
	//로드시 호출되는 함수
	override func awakeFromNib() {
        super.awakeFromNib()
        // Initialization code
    }
    override func setSelected(_ selected: Bool, animated: Bool) {
		//선택한 상대가 바뀔때마다 호출
        super.setSelected(selected, animated: animated)
        // Configure the view for the selected state
    }
}
```

## DetailViewController.swift

---

```swift
//
//  DetailViewController.swift
//  MovieJYJ
//
//  Created by 소프트웨어컴퓨터 on 2021/06/01.
//
import UIKit
import WebKit
class DetailViewController: UIViewController {
    @IBOutlet weak var nameLabel: UILabel!
    @IBOutlet weak var webView: WKWebView!
    var movieName = ""
    override func viewDidLoad() {
        super.viewDidLoad()
        //nameLabel.text = movieName
        navigationItem.title = movieName
        //url뒤에 해당 row의 영화 이름을 추가
        let urlKorString = "https://search.naver.com/search.naver?where=nexearch&sm=top_hty&fbm=0&ie=utf8&query="+movieName
        //쿼리 URL구성 요소에서 허용되는 문자 집합을 반환한다.
        let urlString = urlKorString.addingPercentEncoding(withAllowedCharacters: .urlQueryAllowed)!
        guard let url = URL(string:urlString) else { return }
        let request = URLRequest(url:url)
        webView.load(request)
    }
}
```

## MapViewController.swift

---

```swift
//
//  MapViewController.swift
//  MovieJYJ
//
//  Created by 소프트웨어컴퓨터 on 2021/06/01.
//
import UIKit
//webView사용을 위한 WebKit포함
import WebKit
class MapViewController: UIViewController {
    @IBOutlet weak var webView: WKWebView!
    override func viewDidLoad() {
        super.viewDidLoad()
        //한글이 들어간 URL은 인식에 오류가 있음->.urlQueryAllowed를 사용해
        //쿼리 URL구성 요소에 허용되는 문자집합 반환
       let urlKorString = "https://map.naver.com/v5/search/영화관"
       let urlString = urlKorString.addingPercentEncoding(withAllowedCharacters: .urlQueryAllowed)!
       guard let url = URL(string:urlString) else { return }
       let request = URLRequest(url:url)
       webView.load(request)
    }
}
```

## CinemaViewController.swift

---

```swift
//
//  CinemaViewController.swift
//  MovieJYJ
//
//  Created by 소프트웨어컴퓨터 on 2021/06/10.
//

import UIKit

class CinemaViewController: UIViewController {
    var cinemaSite = ""	//시네마의 url을 담는 변수 초기화
    @IBAction func actLotteCinema(_ sender: UIButton) {	//buttonLotte의 액션함수(클릭시 함수가 호출됨)
        cinemaSite = "https://www.lottecinema.co.kr/NLCMW"	//url에 롯데시네마 모바일 웹 사이트 대입
    }
    @IBAction func actCGV(_ sender: UIButton) {		//buttonCGV의 액션함수
        cinemaSite = "https://m.cgv.co.kr"    }		//CGV의 모바일 웹 사이트가 대입됨
    @IBAction func actMegaBox(_ sender: UIButton) {	//buttonMegaBox의 액션함수
        cinemaSite = "https://m.megabox.co.kr"    }	//Megabox 웹 홈페이지 사이트 대입
//다른 viewController로 값을 전송하는 prepare 함수 구현
//지금의 viewController와 이동할 viewController사이 segue가 연결되어있어야한다.
    override func prepare(for segue: UIStoryboardSegue, sender: Any?) {
//guard let으로 옵셔널 바인딩과 as?를 사용해 넘겨줄 viewController로 다운캐스팅 
       guard let dest = segue.destination as? CinemaSiteViewController else{ return }
       dest.SiteURL = cinemaSite  //viewController의 SiteURL변수에 선택된 url대입
    }  
}
```

## CinemaSiteViewController.swift

---

```swift
//
//  cinemaSiteViewController.swift
//  MovieJYJ
//
//  Created by 소프트웨어컴퓨터 on 2021/06/10.
//

import UIKit

import WebKit	//WebView를 사용하기 위한 WebKit추가

class CinemaSiteViewController: UIViewController {
    var SiteURL = ""	//URL변수 초기화
    @IBOutlet weak var CinemaSite: WKWebView!
    override func viewDidLoad() { //View가 load됨
        super.viewDidLoad()	//상속받은 UIViewController의 viewDidLoad()함수 호출
        let urlString = SiteURL	//SiteURL값을 대입
        guard let url = URL(string:urlString) else { return }  //옵셔널 바인딩으로 url을 넘겨줌
        let request = URLRequest(url:url)
        CinemaSite.load(request)        //사이트를 불러옴
    }
}
```