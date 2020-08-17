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

    ```java
    int[] intArray = null;
    ```
    *널값으로 초기화 배열변수를 변수[인덱스]로 읽거나 저장 : NullPointerException 발생

## 배열의 생성 방법

1. 값 목록으로 배열 생성
    -> 타입[] 변수 = {값1, 값2, 값3...};
    예제)
    ```java
    package sec02.exam01;
    public class ArrayCreateByValueListExample1 {
        public static void main(String[] args) {
            int[] scores = { 83, 90, 87 };      //값목록으로 배열 생성
            
            System.out.println("scores[0] : " + scores[0]); //0번 인덱스의 값
            System.out.println("scores[1] : " + scores[1]); //1번 인덱스의 값
            System.out.println("scores[2] : " + scores[2]); //2번 인덱스의 값
            
            int sum = 0;
            for(int i=0; i<3; i++) {
                sum += scores[i];
            }
            System.out.println("총합 : " + sum);		
            double avg = (double) sum / 3;
            System.out.println("평균 : " + avg);
        }
    }
    ```
    실행결과)

    ![Image Alt 참조타입_배열1]({{"/assets/img/posting/Array_1.png"| relative_url}})

1. new 연산자로 배열 생성
    ->타입[] 변수 = new 타입[길이]; (길이:배열이 저장할 수 있는 값의 개수)
        *값의 목록을 가지고 있진 않지만, 향후 값들을 저장할 배열을 미리 만들고 싶을 때 사용한다.
    예제)
    ```java
    package sec02.exam02;
    public class ArrayCreateByValueListExample2 {
        public static void main(String[] args) {
            int[] scores;
            scores = new int[] { 83, 90, 87 };	//new 연산자로 배열 생성
            int sum1 = 0;
            for(int i=0; i<3; i++) {
                sum1 += scores[i];
            }
            System.out.println("총합 : " + sum1);	
            
            int sum2 = add( new int[] { 83, 90, 87 } );	//값 목록으로 사용한 배열은 add()사용 불가
            System.out.println("총합 : " + sum2);	
            System.out.println();
        }
        
        public static int add(int[] scores) {
            int sum = 0;
            for(int i=0; i<3; i++) {
                sum += scores[i];
            }
            return sum;
        }
    }
    ```    
    실행결과)

     ![Image Alt 참조타입_배열2]({{"/assets/img/posting/Array_2.png"| relative_url}})


