# open API를 이용한 tableView

# open API?

---

→ `**SOAP**`나 `**RESTful 형식**`을 사용하여 공공 컨텐츠를 제공하는 것을 말함

→ REST나 SOAP방식 중 선택적으로 호출 가능하며 REST방식의 응답형식은 `XML` 과 `JSON` 방식을 지원함. 

출처) [XML과 JSON 차이](http://tcpschool.com/json/json_intro_xml)

## SOAP vs REST

---

출처) [SOAP와 RESTful](https://www.redhat.com/ko/topics/integration/whats-the-difference-between-soap-rest)

`SOAP` : SOAP(Simple Object AccessProtocol)는 다른언어로 다른 플랫폼에서 빌드된 애플리케이션이 통신할 수 있도록 설계된 최초의 표준 프로토콜이다. 프로토콜이기 때문에 복잡성,오버헤드가 증가될 수 있어 페이지 로드 시간이 길어질 수 있다. 

`RESTful형식`  - 서버에서 데이터를 받으려면 서버에서 제공하는 명세에 따라 요청해야함

: REST(Representational State Transfer)는 HTTP기반 소프트웨어 아키텍쳐 스타일로 RESTful은 REST설계 지침을 따르는 웹서비스를 말한다.  

- REST아키텍쳐에 적용되는 6가지 제한 조건
    1. 인터페이스 일관성(Uniform interface) 
        - URI를 보고 수행하는 동작을 알 수 있음
        - id와 리소스 이외의 정보를 URI에 넣으면 안됨
        - 동사를 넣지 않고 명사만 사용한다.
    2. 무상태(Stateless) : 각 요청 간 클라이언트의 상태정보가 서버에 저장되면 안됨
    3. 캐시 처리 가능(Cacheable) : 클라이언트는 응답을 캐싱할 수 있어야함
    4. 계층화(Layered System) : 서버를 다중계층으로 구현 가능
    5. Code on demand(optional) : 자바스크립트로 서버가 클라이언트를 실행시킬 수 있는 로직을 전송해 기능을 확장 시킬 수 있어야 함
    6. 클라이언트/서버 구조 : 아키텍쳐를 단순화 시키고 작은 단위로 분리함으로 클라이언트-서버의 각 파트가 독립적으로 개선될 수 있도록 해줌

: 서버에 요청하는 정보 타입은 CRUD타입(Create,Read,Update,Delete)을 사용

- SOAP와 REST의 차이점

    →  대부분의 레거시 시스템에서 SOAP를 준수하며, REST는 그보다 뒤에 고려하거나 웹 기반 시나리오에서의 더 빠른 대안으로 여기는 경우가 많음. (SOAP는 프로토콜로 로드시간이 길어질 수 있기 때문)

    → REST는 유연한 구현을 제공하는 가이드라인 세트고, SOAP는 XML 메시징과 같은 특정 요건이 있는 프로토콜이다.

# open API 사용법

---

## 영화진흥위원회 open API사용방법

1. [영화진흥 위원회](https://www.kobis.or.kr/kobisopenapi/homepg/main/main.do) 홈페이지 가입 후 [키 발급/관리]에서 키를 발급받는다.

![{{"/assets/img/posting/Study_iOS_img/2021-06-05-iOS-study-practice-second/Untitled.png"}}]({{"/assets/img/posting/Study_iOS_img/2021-06-05-iOS-study-practice-second/Untitled.png"}})

2.  응답 예시 처럼 json?key=발급받은키&targetDt=확인날짜(-1일) 형태로 사용한다.

![{{"/assets/img/posting/Study_iOS_img/2021-06-05-iOS-study-practice-second/Untitled1.png"}}]({{"/assets/img/posting/Study_iOS_img/2021-06-05-iOS-study-practice-second/Untitled1.png"}})

3. code beutify를 사용해 데이터를 깔끔하게 확인 할 수 있다.

![{{"/assets/img/posting/Study_iOS_img/2021-06-05-iOS-study-practice-second/Untitled2.png"}}]({{"/assets/img/posting/Study_iOS_img/2021-06-05-iOS-study-practice-second/Untitled2.png"}})

# Xcode에서의 사용법

---

![{{"/assets/img/posting/Study_iOS_img/2021-06-05-iOS-study-practice-second/Untitled3.png"}}]({{"/assets/img/posting/Study_iOS_img/2021-06-05-iOS-study-practice-second/Untitled3.png"}})

```swift
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
}
```

데이터 얻는법

```swift
class ViewController: UIViewController,UITableViewDelegate,UITableViewDataSource {
    @IBOutlet weak var table: UITableView!
    var movieData : MovieData?

    var movieURL = 
"https://www.kobis.or.kr/kobisopenapi/webservice/rest/boxoffice/searchDailyBoxOfficeList.json?key=발급받은키&targetDt="//20210525
    override func viewDidLoad() {
        super.viewDidLoad()
        // Do any additional setup after loading the view.
        table.delegate = self
        table.dataSource = self        
        movieURL += makeYesterdayString()
        getData()
    }

....
```

```swift
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
                        print(decodeData.boxOfficeResult.dailyBoxOfficeList[0].movieNm)
                        print(decodeData.boxOfficeResult.dailyBoxOfficeList[0].audiCnt)
                        self.movieData = decodeData //uses self. inside closure
                        DispatchQueue.main.async{
                            self.table.reloadData()
                        }
                    }catch{
                        print(error)
                    }
                }
            }
            //task 시작하기(task.resume())
            task.resume()
        }
    }
```

## 앱 로드할때마다 자동적으로 날짜 동기화

---

```swift
func makeYesterdayString() -> String
    {
        let y = Calendar.current.date(byAdding: .day, value: -1, to: Date())!
        let dateF = DateFormatter()
        dateF.dateFormat = "yyyyMMdd"
        let day = dateF.string(from: y)   
        return day
    }
```