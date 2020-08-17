---
layout: post
title: "java복습-참조타입:배열"
featured-img: first-post
---
# 배열
배열은 같은 타입의 데이터를 연속된 공간에 나열하고, 각 데이터에 **인덱스(index)**를 부여해놓은 자료구조이다.  
배열 변수는 참조 변수에 속한다.  
배열도 객체이므로 **힙 영역**에 생성되고 배열 변수는 힙 영역의 배열 객체를 참조하게 된다.

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

## 배열의 길이

배열의 길이를 확인하는 방법.

```java
int [] intArray = { 10, 20, 30};
int num = intArray.length;  //길이를 확인하는 방법(배열 변수.length;)

```

## public static void main(String[] args){...}    

-> 전부터 궁금했었는데 정확한 내용은 모르고 지나갔었다...

**String[] args**는 왜 사용할까?  
->명령라인(명령 프롬포트)에서 위 코드를 java명령어로 실행하면 JVM은 길이가 0인 String 배열을 먼저 생성하고 main()메소드를 호출할 때 매개값으로 전달한다.

![Image Alt String_args]({{"/assets/img/posting/String_args.png"| relative_url}})

매개변수 값은 [Run] - [Run Configurations] 메뉴를 선택하여 사용한다.

![Image Alt Run_Configurations]({{"/assets/img/posting/Run_Configurations.png"| relative_url}})

여기서는 매개변수의 값을 10과 20으로 받았다.    
하지만 이것을 실행하게 되면 String 형인 "10","20"으로 인식하기 때문에 산술연산을 할 수 없다.  
산술연산을 하기 위해서는 문자열들을 **Integer.parsInt()** 메소드를 이용하여 정수로 변환 한다.

예제)
```java
public static void main(String[] args){
    int n = Integer.parseInt(args[0]);
}
```
*정수 변환이 불가능한 문자열을 줬을경우:**NumberFormatException**이 발생한다*

## 객체를 참조하는 배열
기본타입 배열은 각 항목에 직접 값을 갖고있지만  
참조타입 배열은 **각 항목에 객체의 번지를 가지고 있음**  
ex)  
```java
String[] strArray  = new String[3];
strArray[0] = "java";
strArray[1] = "C++";
strArray[2] = "C#";
```  
위의 소스를 그림으로 나타내면 아래와 같다.
![Image Alt 다차원배열]({{"/assets/img/posting/다차원배열.png"| relative_url}})  

따라서 String[] 배열의 항목도 String 변수와 동일하게 취급되어야한다.  
예제)  
```java
public class ArrayReferenceObjectExample {
	public static void main(String[] args) {		
		String[] strArray = new String[3];
		strArray[0] = "Java";
		strArray[1] = "Java";
		strArray[2] = new String("Java");

		System.out.println( strArray[0] == strArray[1]);
		System.out.println( strArray[0] == strArray[2] );    
		System.out.println( strArray[0].equals(strArray[2]) );
	} 
}
```  
이렇게 생성했을 때, strArray[0] == strArray[1]의 결과는 true인가?  
아니면 strArray[1] == strArray[2]의 결과는 true인가?

![Image Alt strArray]({{"/assets/img/posting/strArray_결과.png"| relative_url}})  
String객체를 new 연산자로 생성하게 되면 무조건 새로운 String 객체가 생성되기 때문에 strArray[1] == strArray[2] 의 결과는 **false** 가 나온다.
    결과  
    true  
    false  
    true



