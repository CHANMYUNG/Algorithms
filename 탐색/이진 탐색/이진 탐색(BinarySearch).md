# 이진 탐색(Binary Search)
## 이진 탐색 알고리즘이란?
데이터가 모두 오름차순 **정렬되어있는 상태인 배열에서** 특정한 값 target의 위치를 찾아내는 알고리즘  
데이터의 검색 영역(개수)을 점차 절반으로 줄여나가면서 탐색하는것이 특징  

## 동작
변수명 | 뜻
---|---
mid | 현재 탐색범위의 중간 인덱스. (ex - 탐색 범위가 0~6이라면 (0+6) / 2값인 3)
target | 궁극적으로 찾고자하는 값
arr | n개의 데이터가 들어가있는 배열
n | arr의 원소의 개수
left | 현재 검색 범위의 첫 번째 인덱스
right | 현재 검색 범위의 마지막 인덱스

- arr[mid]와 target을 비교, 같다면 해당 인덱스를 리턴하는것이 기본 원리.  
- 만약 `arr[mid] > target`이 성립한다면 타겟값은 left부터 **mid - 1** 사이에 존재함을 의미하는 것이므로 배열에서 탐색할 범위를 (left ~ mid - 1)로 축소
- 만약 `arr[mid] < target`이 성립한다면 타겟값은 배열의 **mid + 1** 부터배열의 마지막 원소 사이에 존재하는 것이므로 배열에서 탐색할 범위를 (mid + 1 ~ right)로 축소
- 위 과정을 반복
- left > right이 성립하는 경우 범위를 좁히다 더이상 탐색할 수 없다(찾고자 하는 값이 존재하지 않는다)는 의미이므로 -1을 리턴

## 구현
#### Java
```java
// java 'BinarySearch.java'

public class BinarySearch {
  public static void main(String[] args) {
    int arr[] = new int[] {1, 2, 10, 22, 777, 1515 };
    int target = 1515;

    System.out.println(binarySearchFunc(arr, target, 0, 5));
    // it prints 5

    System.out.println(binarySearchFunc(arr, -220, 0, 5));
    // it prints -1
  }

  private static int binarySearchFunc(int arr[], int target, int left, int right) {
    int mid = (left + right) / 2;
    if (left > right) return -1;
    if (arr[mid] == target) return mid;
    if (arr[mid] > target) return binarySearchFunc(arr, target, mid + 1, right);
    else return binarySearchFunc(arr, target, left, mid - 1);

  }
}
```
#### C
```c
#include <stdio.h>
int binarySearchFunc(int [], int, int, int);

int main()
{
    int arr[] = int[] {1, 2, 10, 22, 777, 1515 };
    int target = 1515;

    printf("%d\n", binarySearchFunc(arr, target, 0, 5));
    // it prints 5

    printf("%d\n", binarySearchFunc(arr, -220, 0, 5));
    // it prints -1

    return 0;
}

int binarySearchFunc(int arr[], int target, int left, int right) {
    int mid = (left + right) / 2;
    if (left > right) return -1;
    if (arr[mid] == target) return mid;
    if (arr[mid] > target) return binarySearchFunc(arr, target, mid + 1, right);
    else return binarySearchFunc(arr, target, left, mid - 1);
}
```

## 시간복잡도
수행 횟수 = k  
데이터의 개수 = N

- 탐색 시작 당시의 데이터의 개수  
  ![](https://latex.codecogs.com/gif.latex?N)  
- 탐색 1회 수행 후 데이터의 개수  
  ![](https://latex.codecogs.com/gif.latex?%5Cfrac%20%7B%201%20%7D%7B%202%20%7D%20N)  
- 탐색 2회 수행 후 데이터의 개수  
  ![](https://latex.codecogs.com/gif.latex?%5Cfrac%20%7B%201%20%7D%7B%202%20%7D%5E2%20N)    
- 탐색 k회 수행 후 데이터의 개수  
  ![](https://latex.codecogs.com/gif.latex?%5Cfrac%20%7B%201%20%7D%7B%202%20%7D%5Ek%20N)  
  
  
탐색 종료를 위해서는 데이터의 개수가 1이 되어야 하므로  
![](https://latex.codecogs.com/gif.latex?%5Cfrac%20%7B%201%20%7D%7B%202%20%7D%20%5E%7B%20k%20%7DN%3D1)  
양 쪽에 2^k를 곱하면  
![](https://latex.codecogs.com/gif.latex?N%3D2%5Ek)  
결국 k는  
![](https://latex.codecogs.com/gif.latex?k%3Dlog_%7B2%7DN)  
  
따라서 구하고자하는 시간복잡도는  
![](https://latex.codecogs.com/gif.latex?O%28logN%29)  
이다.