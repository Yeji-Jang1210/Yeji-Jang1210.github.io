---
layout : post
title : "Selection_Sort구현"
featured-img: JSP-study
categories : [Data_Structure]
---
# Selection_Sort 구현
---
Selection_Sort는 배열에서 최소값을 찾아 최소값이 있던 자리와 맨 앞의 배열의 자리를 바꿔주면서 정리하는 배열이다. 따라서 최소값의 주소를 알아야 하기 때문에 pointer min을 사용했다.  
n++ 하면서 포인터의 위치도 n++만큼 이동한다.  
그리고 제일 안쪽의 for문에서 포인터 min이 가르키는 주소의 값과 비교하여 최소값을 찾으면 min은 최소값의 주소를 가진다.  
```c++
#include <stdio.h>
void selection_sort(int array[], int size);

int main(void) 
{
    int arr[] = { 1,3,4,2,5,6 };
    printf("before:");
    for (int i = 0; i < 6; i++) {   //before selection sort
        printf("%i", arr[i]);
    }
    printf("\n");
    printf("--- selection sort ---\n");
    selection_sort(arr, 6);
}

void selection_sort(int arr[], int size) 
{
    for (int n = 0; n < size; n++) 
    {
        int tmp = 0;
        int *min = arr+n;   
        for (int i = n+1; i < size; i++)    //n의 값과 다음값 비교
        {
            if (*min > arr[i])  //최소값이 더 크면
            {
                min = &arr[i];  //비교하는 값의 주소를 가짐
            }
        }
        tmp = arr[n];   //임시공간 tmp는 n의 자리의 값을 가짐
        arr[n] = *min;  //최소값을 n번째 대입
        *min = tmp;     //min이 가르키는 주소에 원래 n의 주소에 있던 값을 대입
        printf("%i번째 : ", n + 1);
        for(int j = 0; j < size; j++) 
        {
            printf("%i", arr[j]);
        }
        printf("\n");
    }
}
```