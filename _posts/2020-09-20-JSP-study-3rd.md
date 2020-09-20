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
