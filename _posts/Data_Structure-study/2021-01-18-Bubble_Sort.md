---
layout : post
title : "Bubble_Sort구현"
featured-img: JSP-study
categories : [Data_Structure]
---
# Bubble Sort 구현
---  
  보통의 경우 bubble sort는 Omega(n^2)가 걸리지만 만약 비교가 끝났을 경우 for문을 탈출하면  
  Omega(n)까지 줄일 수 있다. 또한 정렬이 한번 끝날때마다 끝 번호는 정렬을 할 필요가 없다.  
```c++
    #include <stdio.h>
    #include <stdbool.h>	//bool type
    #include <time.h>	//시간함수 추가
    void bubble_sort(int array[], int size);

    int main(void)
    {
<<<<<<< HEAD
        clock_t start = clock();	//시작
        int arr[] = {1,2,3,4,5,6 };
        printf("before : ");
        for (int i = 0; i < 6; i++)
        {
            printf("%i", arr[i]);
        }
        printf("\n");
        bubble_sort(arr, 6);
        printf("\nbubble sort:");
        for (int i = 0; i < 6; i++) 
        {
            printf("%i", arr[i]);
        }
        printf("\n");
        clock_t end = clock();	//종료
        printf("Time: %lf\n", (double)(end - start) / CLOCKS_PER_SEC);	//걸리는 시간
=======
    clock_t start = clock();	//시작
    int arr[] = {1,2,3,4,5,6 };
    printf("before : ");
    for (int i = 0; i < 6; i++)
    {
    printf("%i", arr[i]);
    }
    printf("\n");
    bubble_sort(arr, 6);
    printf("\nbubble sort:");
    for (int i = 0; i < 6; i++) 
    {
    printf("%i", arr[i]);
    }
    printf("\n");
    clock_t end = clock();	//종료
    printf("Time: %lf\n", (double)(end - start) / CLOCKS_PER_SEC);	//걸리는 시간
>>>>>>> posting
    }
    
    void bubble_sort(int array[], int size) 
    {	
<<<<<<< HEAD
        for (int n = 0; n < size ; n++)
        {	
            int s_size = size;	//비교가 끝날때마다 마지막은 비교할 필요가 x 점점 줄어듬
            bool swap = false;
            for (int i = 0; i < s_size - 1 ; i++)
            {	
              if (array[i] > array[i + 1])	//a>b
              {
              int tmp = 0;
              tmp = array[i];		//a = tmp
              array[i] = array[i + 1];	//b = a
              array[i + 1] = tmp;	//tmp = b
              swap = true;
              }
            }
            if (swap == false) // 교환이 잃어나지 않았을 경우
            {
              break;	//for문 빠져나옴
            }
        printf("%i번째 : ", n + 1);
        for (int j = 0; j < size; j++)
        {
            printf("%i", array[j]);
        }
        printf("\n");
        s_size--;
        }
=======
    for (int n = 0; n < size ; n++)
    {	
    int s_size = size;	//비교가 끝날때마다 마지막은 비교할 필요가 x 점점 줄어듬
    bool swap = false;
    for (int i = 0; i < s_size - 1 ; i++)
    {	
    if (array[i] > array[i + 1])	//a>b
    {
    int tmp = 0;
    tmp = array[i];		//a = tmp
    array[i] = array[i + 1];	//b = a
    array[i + 1] = tmp;	//tmp = b
    swap = true;
    }
    }
    if (swap == false) // 교환이 잃어나지 않았을 경우
    {
    break;	//for문 빠져나옴
    }
    printf("%i번째 : ", n + 1);
    for (int j = 0; j < size; j++)
    {
    printf("%i", array[j]);
    }
    printf("\n");
    s_size--;
    }
>>>>>>> posting
    }
```
