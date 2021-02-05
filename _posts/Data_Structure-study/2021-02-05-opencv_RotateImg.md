---
layout : post
title : "opencv를 활용한 RotationImg구현"
featured-img: JSP-study
categories : [Data_Structure]
---
# opencv 사용
---
opencv는 컴퓨터비전을 목적으로 한 **프로그래밍 라이브러리**이다.  
영상처리나 딥러닝에 유용한 기능이 많아 많이 사용된다.  
[opencv 활용방법](https://diyver.tistory.com/50)을 참고해서 다운받았다.  
나중에 Release로 exe파일을 만들어 cmd로 설치하려면 아래의 파일을 Release디렉토리 안에 넣어주면 된다.  
opencv_world451.dll은 Release파일용이고 opencv_world451.d.dll은 Debug용이다.  
![opencvfile]({{"/assets/img/posting/opencv.png"| relative_url}})  

# opencv 라이브러리를 활용한 이미지 회전
---
[Yeji-jang1210_opencv_github_source](https://github.com/Yeji-Jang1210/data_structure/blob/master/RotateImg/RotateImg/RotateImg.cpp)  
소스가 너무 길기 때문에 전체소스는 url로 대체하고 이미지를 회전하기 위한 소스를 따로 정리했다.  <br>

## 1. opencv로 이미지 읽기 및 열기
---
1. opencv라이브러리를 사용하기 위해 라이브러리를 include해준다.  

```c++
#include <opencv2/core.hpp>
#include <opencv2/imgcodecs.hpp>
#include <opencv2/highgui.hpp>

using namespace cv;
```

<br>

2. 이미지 경로 및 읽기  

```c++
 String imgPath = samples::findFile(imname);  //이미지 경로 저장
    Mat img = imread(imgPath, IMREAD_GRAYSCALE);        //imread(파일이름의 주소,색상형식)
    if (img.empty()) 
    {
        printf("파일을 읽을 수 없음");
        return 1;
    }
```
<br>

samples::findFile()은 cv namespace안에있는 samples namespace의 findFile()을 사용한다는 뜻이다.  
findFile(imname)은 이미지 파일의 경로를 저장하는데 상대경로로 파일을 찾아 경로를 저장한다.  
아래 그림은 [findFile](https://docs.opencv.org/master/d6/dba/group__core__utils__samples.html#ga3a33b00033b46c698ff6340d95569c13)의 설명이다.  
![findFile]({{"/assets/img/posting/findfile.png"| relative_url}})   <br>
imread()는 이미지경로를 읽어 색상을 어떤형식으로 줄 것인지 읽는 함수이다.  
색상형식은 여러개가 있는데 여기서는 0-255사이의 숫자만 읽어 회전하기 때문에 IMREAD_GRAYSCALE을 사용했다.  
[imread 색상형식](https://docs.opencv.org/master/d8/d6a/group__imgcodecs__flags.html#gga61d9b0126a3e57d9277ac48327799c80af660544735200cbe942eea09232eb822)  

<br>

3. 이미지 출력  

```c++
imshow("img", img);//imshow(디스플레이 이름,mat형식의 이미지 표시)
waitKey();
```

imshow는 윈도우창에 띄울 제목(이름)을 표시하고 이미지를 띄운다.  
그리고 waitKey를 사용해 얼마나 지속시킬건지 정하는데 위처럼 아무것도 적지 않는 다면 다른 키를 입력하기 전까지 이미지를 띄우는 것을 지속시킨다는 뜻이다.  

<br><br>

## 2. **이미지 회전**
---
```c++
    for (int i = 0; i < sizeY; i++)
    {
        for (int j = 0; j < sizeX; j++)
        {
            c = cos(radian) * (j - reBaseX) + -sin(radian) * (i - reBaseY) + baseX; //열 
            r = sin(radian) * (j - reBaseX) + cos(radian) * (i - reBaseY) + baseY;  //행
            if ((c >= 0 && c < x) && (r >= 0 && r < y))
            {
                img3.at<uchar>(i, j) = estimateValue(img, r, c);
            }
            else
            {
                img3.at<uchar>(i, j) = 0;
            }
        }
    }
```  
이미지의 구조는 픽셀로 되어있는데 이 픽셀의 집합을 행렬로 표현한 것이 이미지이다.  
따라서 opencv안에 있는 Mat클래스는 Matrix의 줄임말이다.  
rotationImg함수로 이미지와 각도를 받아 회전시키는데 위의 소스는 함수의 일부이다.  
값을 받아와 실질적으로 회전을 하는 for문인데 회전행렬을 하기 위해서는 cos와 sin이 필요해 **math.h**라이브러리도 include했다.  
[회전행렬](https://gaussian37.github.io/math-la-rotation_matrix/)을 참고하여 작성했다.  
회전시킬 이미지를 띄울 Mat img를 하나 만든 후 [i,j]를 회전시켜 그에 해당하는 값을 원본에서 가져오는데
이렇게 할경우 겹치는 값이 생기기 때문에 최대한 근사한 값을 찾아 대입해줘야한다.  
그래서 estimateValue라는 함수를 만들어 값을 추측해 대입한다.  
아래 그림은 estimateValue의 원리이다.  
픽셀과 픽셀사이의 값을 이용했는데 픽셀의 위치와 색은 반비례하기 때문에 값을 추측할 수 있다.  
![estimatepixel]({{"/assets/img/posting/estimatepixel.png"| relative_url}})   <br>
reBaseX는 이미지가 회전했을때 잘리지 않도록 중심점을 다시 잡아준 것이다.  <br><br>

## 3. 회전한 이미지의 size
---
회전한 이미지의 크기는 원래있던 각 꼭지점을 회전시켜 얻어낸 최소값과 최대값을 찾아 회전된 이미지의 크기를 찾아낸다.  
```c++
void returnSize(double radian, int x,int y, int *sizeX, int *sizeY,int baseX,int baseY) 
{

    //0,0
    int c_dot1 = cos(radian) * (0 - baseX) + sin(radian) * (0 - baseY) + baseX;
    int r_dot1 = -sin(radian) * (0 - baseX) + cos(radian) * (0 - baseY) + baseY;

    //0,x-1
    int c_dot2 = cos(radian) * ((x - 1) - baseX) + sin(radian) * (0 - baseY) + baseX;
    int r_dot2 = -sin(radian) * ((x - 1) - baseX) + cos(radian) * (0 - baseY) + baseY;

    //y-1,0
    int c_dot3 = cos(radian) * (0 - baseX) + sin(radian) * ((y - 1) - baseY) + baseX;
    int r_dot3 = -sin(radian) * (0 - baseX) + cos(radian) * ((y - 1) - baseY) + baseY;

    //y-1,x-1
    int c_dot4 = cos(radian) * ((x - 1) - baseX) + sin(radian) * ((y - 1) - baseY) + baseX;
    int r_dot4 = -sin(radian) * ((x - 1) - baseX) + cos(radian) * ((y - 1) - baseY) + baseY;

    *sizeX = addRotationImgSize(c_dot1, c_dot2, c_dot3, c_dot4);
    *sizeY = addRotationImgSize(r_dot1, r_dot2, r_dot3, r_dot4);
}
    int addRotationImgSize(int dot1, int dot2, int dot3, int dot4) 
{
    int dotArr[4] = { dot1, dot2, dot3, dot4 };
    int min = dotArr[0];
    int max = dotArr[0];
    int tmp = 0;
    for (int i = 1; i < 4; i++) 
    {
        if (dotArr[i] > max)
        {
            max = dotArr[i]; 
        }
        if (dotArr[i] < min) 
        {
            min = dotArr[i];
        }
    }
    int size = max-min;
    return size;
}
```
## 4. 결과
---
![result]({{"/assets/img/posting/result.png"| relative_url}})   <br>