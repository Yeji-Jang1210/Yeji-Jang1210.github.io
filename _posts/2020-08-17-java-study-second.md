---
layout: post
title: "java복습-참조타입:배열"
featured-img: first-post
---
# 배열
배열은 같은 타입의 데이터를 연속된 공간에 나열하고, 각 데이터에 **인덱스(index)**를 부여해놓은 자료구조이다.

배열 변수는 참조 변수에 속한다. 배열도 객체이므로 **힙 영역**에 생성되고 배열 변수는 힙 영역의 배열 객체를 참조하게 된다.

배열의 선언은 두가지 방법으로 가능하다.

## 배열의 선언 방법
1. 타입[] 변수;

    ```java
    int[] intArray;
    double[] doubleArray;
    String[] strArray;
    ```

1. 타입 변수[];

    ```java
    int intArray[];
    double doubleArray[];
    String strArray[];
    ```

1. null값으로 초기화 : 타입[] 변수 = null;

