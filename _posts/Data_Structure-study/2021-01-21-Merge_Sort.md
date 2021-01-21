---
layout : post
title : "Merge_Sort구현"
featured-img: JSP-study
categories : [Data_Structure]
---
# Merge_Sort
---
Merge_Sort는 재귀함수를 사용해 원소가 나눠질 수 없을 때까지 나눈 후 함수가 실행이 완료되고 돌아오면서 원소를 비교하고 병합하는 원리이다.  <br>
## divide
---
merge_sort(array,start,mid); : end값을 mid값으로 사용해 함수를 반씩 줄여가기 때문  
merge_sort(array.mid+1,end); : 처음 시작값을 mid+1로 사용해 뒤쪽을 반씩 줄임  
![Image Alt merge_sort]({{"/assets/img/posting/merge_sort.png"| relative_url}})   <br>

## Merge
---
merge 함수 원리
값을 두개씩 비교하면서 l이 m을 만나거나 r_mid(mid+1)이 r을 만나면 while문을 종료하고
아직 만나지 않은 쪽(비교가 되지 않은 값)을 복사해서 넣는다.  
그리고 비교하지 않은 값들을 array(원래 배열)값을 복사해서 넣는다.  
![Image Alt merge_sort]({{"/assets/img/posting/merge_sort_2.png"| relative_url}})   <br>

```c++
#include <stdio.h>
#define ARRAY_LENGTH 7
int sorted_arr[ARRAY_LENGTH];
void merge_sort(int array[], int start, int end);
void merge(int array[], int left, int mid, int right);

int main(void) 
{
    int arr[] = { 4,1,3,6,9,5,2 };

    printf("before: ");
    for (int i = 0; i < ARRAY_LENGTH; i++)
    {
        printf("%i ", arr[i]);
    }
    printf("\n");

    printf("Merge_Sort: ");
    printf("\n");
    merge_sort(arr, 0, ARRAY_LENGTH - 1);
}

void merge_sort(int array[], int start, int end)     //array[n]일때 end = n-1
{
    int mid;
    if (start < end) //시작과 끝이 같지 x
    {
        mid = (start + end) / 2;            //중간값 재계산
        merge_sort(array, start, mid);      //left divide
        merge_sort(array, mid + 1, end);    //right divide
        merge(array, start, mid, end);      //병합 필요
    }
    for (int i = 0; i < ARRAY_LENGTH; i++)
    {
        printf("%i ", array[i]);
    }
    printf("\n");

}
void merge(int array[], int left, int mid, int right) 
{   
    int l = left;
    int m = mid;
    int r = right;
    int r_mid = m + 1;
    int i = l;

    while (l <= m && r_mid <= r)
    {
        if (array[l] < array[r_mid])    //a<b면 제일 왼쪽 자리에 a대입 후 a++
        {
            sorted_arr[i] = array[l];
            l++;
        }
        else
        {
            sorted_arr[i] = array[r_mid];  //a>b면 제일 왼쪽 자리에 b대입 후 b++ 
            r_mid++;
        }
        i++;
    }
    //남은 숫자 배열에 대입
    if (l > m)
    {
        while (r_mid <= r)
        {
            sorted_arr[i++] = array[r_mid++];
        }
    }
    else 
    {
        while (l <= m)
        {
            sorted_arr[i++] = array[l++];
        }
    }

    for (int i = left; i<=right ; i++) //l부터 r까지 원래 배열로 복사
    {
        array[i] = sorted_arr[i];
    }

}

```  
<br>

## Result
---
![Image Alt merge_sort_result]({{"/assets/img/posting/merge_sort3.png"| relative_url}})   <br>