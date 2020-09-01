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
    <br>

    ![Image Alt IDEA_다운로드]({{"/assets/img/posting/Study_JSP_img/Study_JSP_post_1/IDEA_다운.png"| relative_url}})

    라이센스창에 들어가서 다운로드를 누르고 받으면 된다.  


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

    <br>
    *근데 나중에 실행해보니 다른걸 받아서 안뜨는거였다.. 설치 방법에서는 별 다른 것은 없다.*



1. apache-tomcat-9.0.37
    압축을 푼 후, C드라이브나 D드라이브에 추가한다.  
    *C드라이브는 보통 window에서 보호가 되어있으므로 D드라이브에 추가하는 것을 권한다.*    
    
    ![Image Alt 기본개발환경구축_7]({{"/assets/img/posting/Study_JSP_img/Study_JSP_post_1/HomeDirectory.png"| relative_url}})  

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
![Image Alt 기본개발환경구축_9]({{"/assets/img/posting/Study_JSP_img/Study_JSP_post_1/IDEA_HomeDirectory.png"| relative_url}})  

JetBrains가 아닌 <u>IntelliJ IDEA 2020.2.1</u>가 홈이다. 확인은 [시스템속성]-[고급]-[환경변수]에서 확인이 가능하다.  
  
<br>
<br>

# IDEA 실행
---

1. 우측하단쪽에 톱니바퀴 모양 옆 [Configure]을 누르면 PlugIn이 있는데 들어가면 사용하고 싶은 것들을 Enable/Disable할지 설정 할 수 있다.  
설정이 끝나면 NewProject로 만들어준다.  
    ![Image Alt IDEA_실행]({{"/assets/img/posting/Study_JSP_img/Study_JSP_post_1/IDEA_실행2.png"| relative_url}})   

1. NewProject를 누르면 Enable한것들이 나온다.  
우리는 JAVA를 사용해야 하므로 [Java Enterprise]를 누른 후 Test Runner을 TestNG로 설정해준다(사진에는 TestNG설정 전이다.)  

    ![Image Alt IDEA_실행2]({{"/assets/img/posting/Study_JSP_img/Study_JSP_post_1/IDEA_실행1.png"| relative_url}})      

1. Web Profile을 클릭후 next 로 넘어간다. 
    ![Image Alt IDEA_실행3]({{"/assets/img/posting/Study_JSP_img/Study_JSP_post_1/IDEA_실행3.png"| relative_url}})   

1. Group과 Artifact를 설정해준다. Artifact를 바꿔주면 자동적으로 Name이 바뀐다.  
    ![Image Alt IDEA_실행4]({{"/assets/img/posting/Study_JSP_img/Study_JSP_post_1/IDEA_실행4.png"| relative_url}})     

1.  최종화면
    ![Image Alt IDEA_실행5]({{"/assets/img/posting/Study_JSP_img/Study_JSP_post_1/IDEA_실행5.png"| relative_url}})   

<br>
<br>

# JSP파일 만들기
---  
<br>

![Image Alt JSP생성]({{"/assets/img/posting/Study_JSP_img/Study_JSP_post_1/JSP생성.png"| relative_url}}) 

[webapp파일]-[New]-[JSP/JSPX]를 클릭하면 생성이 가능하다.  

<br>
<br>

# JSP파일 실행하기
---  
<br>
<br>

JSP파일을 실행하려면 템플릿이 필요하다. TomCat을 사용하기 위해 [File]-[Settings]-[Plugins]에 TomCat을 검색해 활성화 해준다.  
     ![Image Alt JSP실행1]({{"/assets/img/posting/Study_JSP_img/Study_JSP_post_1/JSP실행1.png"| relative_url}})    

<br>
<br>

1. 우측 상단에 [Add Configuration]을 누른다.  

1. Templates에 [Tomcat]-[local]을 선택 후 [Create configuration]을 눌러준다.  
     ![Image Alt JSP실행2]({{"/assets/img/posting/Study_JSP_img/Study_JSP_post_1/JSP실행2.png"| relative_url}})    

1. 사용하고 있는 톰캣 버전을 Name으로 지정해주고 tomcat의 home directory를 지정해준다.(tomcat home directory는 위에 나와있다.)  
     ![Image Alt JSP실행3]({{"/assets/img/posting/Study_JSP_img/Study_JSP_post_1/JSP실행3.png"| relative_url}})   

1. [Deployment]에 들어가 +버튼을 눌러 아래와 같이 추가해 주고 [ok]를 눌러준다.  
    ![Image Alt JSP실행4]({{"/assets/img/posting/Study_JSP_img/Study_JSP_post_1/JSP실행4.png"| relative_url}})   

1. [tomcat9.0.37]옆 아이콘을 클릭하면 tomcat 서버가 실행되면서 배포가 되며 동작이 된다.  
    ![Image Alt JSP실행5]({{"/assets/img/posting/Study_JSP_img/Study_JSP_post_1/JSP실행5.png"| relative_url}})   

<br>
<br>

※수정후 저장이 된다고 해서 바로 고쳐지는 것이 아니다.  
    ![Image Alt JSP실행6]({{"/assets/img/posting/Study_JSP_img/Study_JSP_post_1/JSP실행6.png"| relative_url}})   
[Deploy]버튼을 눌러 실행해줘야한다.(Undeploy:배포 취소)    


