---
layout : post
title: "JSP 공부:사용자 요청 처리"
featured-img: JSP-study
categories : [JSP]
---

# HTTP
---
* 하이퍼미디어 정보 시스템을 위한 **통신규약**으로 클라이언트의 요청과 서버의 응답을 처리하는 `클라이언트-서버` 방식을 사용한다.  
    * [`클라이언트-서버`](https://yeji-jang1210.github.io/JSP-study-2nd/)
* 무상태(stateless) 프로토콜이다. 상태를 보관하지 않는다.
* HTTP는 올바른 전송을 위해 `TCP/IP`를 사용한다.  
    * [`TCP/IP`](https://namu.wiki/w/TCP/IP)
* [HTTP에 대한 더 자세한 정보](https://shlee0882.tistory.com/107)  
<br>

## HTTP 메세지(Message)
---
* HTTP 대화의 기본단위(basic unit of HTTP communication)이다. 
<br>

### HTTP 메세지의 구조
---
1. Start-Line
    * Request-Line │ Status-Line
1. Message-Headers
    * {field-name ":" [field-value]}Ｎ
1. CRLF(Carriage Return Life Feed)
    * CR+LF가 합쳐진 문자이다.  
        * CR(Carriage Return) : 현재 라인에서 커서의 위치를 가장 앞으로 옮기는 동작
        * LF(Life Feed) : 커서의 위치는 그대로 두고 종이를 한 라인 위로 옮기는 동작
        * *출저)[CRLF](https://m.blog.naver.com/PostView.nhn?blogId=pthread_join&logNo=220720777376&proxyReferer=https:%2F%2Fwww.google.com%2F)
1. Message Body(메소드의 형태에 따라 다름)
    * entity-body │ entity-body encoded as per Transfer-Encoding
<br>

### **요청** 메시지(Request Message), 요청 포맷의 경우 : 브라우저가 서버에게
---
1. Request-Line
    * `Method` SP `Request-URI` SP `HTTP-Version` CRLF
        * `Method` : HTTP 메소드
            * Option : POST / GET ...
        * `Request-URI` : 웹 서버상 존재하는 자원의 경로
            * URI : `URL`:[위치정보]과 `URN`:[QR코드,바코드 등]을 포함
        * `HTTP-Version` : 프로토콜 버전
1. Request-Headers
    * {field-name ":" [field-value]}Ｎ
1. CRLF
1. [Message-Body(Payload)] : 있을수도 있고 없을수도 있음   
<br>

### **응답** 메세지(Response Message), 응답포맷 : 서버가 클라이언트에게
---
1. Status-Line
    * HTTP-Version SP `Status-Code` SP `Reason-Phrase` CRLF
        * `Status-Code` : [HTTP상태 코드](https://developer.mozilla.org/ko/docs/Web/HTTP/Status)  
            * 대표적인 예) 404 Not Found : URL 오류로 자원을 찾지 못함(클라이언트 오류)
        * `Reason-Phrase` : 상태 코드에 대한 텍스트
1. Response-Headers
    * {field-name ":" [field-value]}Ｎ
1. CRLF
1. Message-Body
    * Content-Encoding(`Content-Type`(data))
        * `Content-Type` : 항목에 지정된 값으로 자원의 종류를 구별해준다. `MIME`사용.  
            * `MIME` : Multipurpose Internet Mail Extensions

## Postman
---
* API 개발을 위한 협동 플랫폼으로 API 개발의 생산성을 높여주는 플랫폼이다.  
<br>  

### 설치
---
* [Postman 경로로 다운받는다.](https://www.postman.com/downloads/)
* 가입을 하면 웹상으로도 Postman을 이용할 수 있다고 한다.  

### 가입
---
![Image Alt Postman_1]({{"/assets/img/posting/Study_JSP_img/Study_JSP_post_3/Postman_1.png"| relative_url}})    
* 설치하고 처음 나오는 화면이다.  
* 구글 아이디로도 다운을 받을 수 있다.   

### 실행
![Image Alt Postman_2]({{"/assets/img/posting/Study_JSP_img/Study_JSP_post_3/Postman_2.png"| relative_url}})  
* 실행화면의 `+`버튼을 눌러 URL을 입력한 후, `Send`버튼을 누른다.  
<br>

![Image Alt Postman_2]({{"/assets/img/posting/Study_JSP_img/Study_JSP_post_3/Postman_3.png"| relative_url}})  
* 깃허브 블로그 주소를 send한 후, [Headers]창의 결과이다. 프로그램 자체에서 프로토콜을 분석해서 웹브라우저 상에서 동작하는 것이 아닌 독립적인 클라이언트 프로그램을 만든 것이다.
* URL옆에 부분은 지금은 [Get]방식으로 되어있는데, 아래 화살표키를 눌러 방법을 바꿀 수 있다.   
* GET과 POST  

| --- | GET | POST |
| 정의 | 서버에 있는 정보를 가져오기 위해 설계된 방법 | 정보를 전달하기 위해 설계된 방법 |
| 크기제한 | 제한이 있음(2048byte) | 제한이 없음 |
| 보안 | URL에 값이 노출되어 보안문제 발생할 수 있음 | URL이 간결, 표시되지 않기 때문에 보안성이 높음 | 
| 캐쉬저장 | 웹 클라이언트들이 캐쉬 저장이 가능 | 캐쉬 저장이 불가 |
| 형식 | URI?"속성=값&속성=값..." |     

* Headers에서 Key와 Value를 추가할 수 있다.   
* 아래 Body와 Header부분은 응답헤더, 응답 바디들을 확인 할 수 있다.  

## 사용자 요청 전송을 위한 HTML 폼 작성
---
1. 쿼리스트링을 이용한 방법
1. <u>폼을 이용한 방법</u>  
ex)  
```html
    <form method="get or post">~</form>
```
<br><br>

## IntelliJ IDEA 한글 문제 해결
---
IntelliJ에서 한글메세지가 정상적으로 표현되지 않을 때 해결하는 방법이다.  

1. [File]-[Settings]-[Editor]-[File and Code Templates]-[other]-[JSP files]를 들어간 후,  "<%@ page contentType="text/html;charset=UTF-8" `pageEncoding="UTF-8"` language="java" %>"로 작성해준다.  
    ![Image Alt JSP_1]({{"/assets/img/posting/Study_JSP_img/Study_JSP_post_3/JSP_1.png"| relative_url}})  
1. 우측상단에 돋보기를 누른 후, [Actions]에 VM을 검색 후, [Edit Custom VM Options]를 클릭 후 창이 나오면 제일 밑에 `-Dfile.encoding=UTF-8`를 작성한 후 재실행 해준다.  
    ![Image Alt JSP_2]({{"/assets/img/posting/Study_JSP_img/Study_JSP_post_3/JSP_2.png"| relative_url}})  
    <br>
1. 한글이 잘 나오는지 확인하기 위해 JSP파일을 새로 만들고 아래부분을 입력했다.  
    ```JSP
    <body>
    <%= "테스트를 실행합니다."%>
    </body>
    ``` 
1. 톰캣을 설정해주고 [RUN]하면 결과가 나온다.         
    ![Image Alt JSP_3]({{"/assets/img/posting/Study_JSP_img/Study_JSP_post_3/JSP_3.png"| relative_url}})  
<br><br>

### IntelliJ 실습하며 생긴 오류
---
localhost:8080/test.jsp로 실행했을때 화면이 위와 같이 나와야하는데  
*http://localhost:8080/Gradle___iducs_jsp201912038___webapp2020_1_0_war/* 이런경로로 들어가야 나오는 상황이 발생했었다.  
이런 경우에는 **Run/Debug Configurations에 들어가 [Tomcat Server]-[Deployment]의 [Application context]를 확인해주자.**  
<br>
![Image Alt JSP_4]({{"/assets/img/posting/Study_JSP_img/Study_JSP_post_3/JSP_4.png"| relative_url}})  
위 그림과 같이 되어있으면 경로를 지우고 **`/`**만 남겨준다.
<br>  
![Image Alt JSP_5]({{"/assets/img/posting/Study_JSP_img/Study_JSP_post_3/JSP_5.png"| relative_url}})  
이부분도 확인해주자.  



