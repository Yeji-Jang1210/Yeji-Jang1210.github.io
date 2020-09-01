---
layout: post
title: "JSP 공부:기본 개발 환경 구축"
featured-img: JSP-study
---

# JSP 기본 개발 환경 구축1 : 다운로드
---
JDK(Java Development Kit) LTS, IDE, Java Web Application Server개발환경 구축.  
1. adoptopenjdk.net에 접속해 필요한 파일을 다운 받는다.  
    주소 : [Adoptopenjdk](https://adoptopenjdk.net/)
    ![Image Alt 기본개발환경구축_1]({{"/assets/img/posting/Study_JSP_img/Study_JSP_post_1/기본개발환경구축_1.png"| relative_url}})  
    **HotSpot이나 OpenJ9가 뭔지 궁금하다면 옆의 <u>Help Me Choose</u>를 누르면 된다.*  

1. IntelliJ IDEA 홈페이지에 접속해 회원가입 후 신청 버튼을 누른다.
    주소 : [IntelliJ IDEA](https://www.jetbrains.com/ko-kr/community/education/#students)
    ![Image Alt 기본개발환경구축_2]({{"/assets/img/posting/Study_JSP_img/Study_JSP_post_1/기본개발환경구축_2.png"| relative_url}})  
    *어찌저찌 라이센스가 등록은 된 것 같다..(영어를 몰라서 조금 복잡했음)*
    대학교 이메일로 등록을 했으면 대학교 메일로 가입하라는 메일이 하나 온다.  
    그리고나서 회원가입을 하면 라이센스가 등록이 되어 교육용 IntelliJ IDEA를 사용 할 수 있는 것 같다.  

1. Apache Tomcat에 접속해 zip파일로 받는다.
    주소 : [Apache Tomcat](http://tomcat.apache.org/download-90.cgi)
    ![Image Alt 기본개발환경구축_3]({{"/assets/img/posting/Study_JSP_img/Study_JSP_post_1/기본개발환경구축_3.png"| relative_url}})    

<br>
<br>
<br>

# JSP 기본 개발 환경 구축1 : 설치
---
![Image Alt 기본개발환경구축_4]({{"/assets/img/posting/Study_JSP_img/Study_JSP_post_1/기본개발환경구축_4.png"| relative_url}})  
세개의 다운받은 파일을 하나씩 설치 해준다.  
<br>

1. OpenJDK11U-jdk_x64_windows_hotspot_11.0.8_10
    더블클릭 후 [Next]-[Next]눌러주고 아래의 그림과 같이 설정해 준다.  
    ![Image Alt 기본개발환경구축_5]({{"/assets/img/posting/Study_JSP_img/Study_JSP_post_1/기본개발환경구축_5.png"| relative_url}})  

1. ideaIE-2020.2.1
    더블클릭 후 [Next]-[Next]눌러주고 컴퓨터에 맞게 [Create Desktop Shortcut]를 설정해주고
    나머지 부분은 확장성을 고려하여 선택해 주면 된다.
    ![Image Alt 기본개발환경구축_6]({{"/assets/img/posting/Study_JSP_img/Study_JSP_post_1/기본개발환경구축_6.png"| relative_url}})  
    [Next]를 누른 뒤 Install을 눌러 설치를 한다.  

    *[시스템]-[시스템속성]-[고급]-[환경변수]에 들어가 보면 환경변수가 Intellij 경로가 추가된 것을 확인할 수 있다*

1. apache-tomcat-9.0.37
    압축을 푼 후, C드라이브나 D드라이브에 추가한다.  
    *C드라이브는 보통 window에서 보호가 되어있으므로 D드라이브에 추가하는 것을 권한다.*    
    ![Image Alt 기본개발환경구축_7]({{"/assets/img/posting/Study_JSP_img/Study_JSP_post_1/기본개발환경구축_7.png"| relative_url}})

1. 마지막으로 재부팅을 해준다.  
<br>
<br>

# JSP 기본 개발 환경 구축2
---
자바의 홈 디렉터리는 bin을 감싸고있는 디렉터리를 말한다.
즉 아래 그림의 경로이다.  
![Image Alt 기본개발환경구축_8]({{"/assets/img/posting/Study_JSP_img/Study_JSP_post_1/기본개발환경구축_8.png"| relative_url}})  

<br>
아래는 IntelliJ IDEA의 홈 디렉터리 경로이다.  
![Image Alt 기본개발환경구축_9]({{"/assets/img/posting/Study_JSP_img/Study_JSP_post_1/기본개발환경구축_9.png"| relative_url}})  

*JetBrains가 아닌 <u>IntelliJ IDEA Educational Edition 2020.2.1</u>가 홈이다. 확인은 [시스템속성]-[고급]-[환경변수]에서 확인이 가능하다.*

