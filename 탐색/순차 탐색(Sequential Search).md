# 순차 탐색 알고리즘(Sequential Search)

## 순차 탐색 알고리즘이란?
정렬되어있지 않은 데이터 배열에서 특정한 데이터를 찾아내는 알고리즘  
배열을 순회하며 타겟 데이터와 비교하는 가장 원시적인 방법을 사용함  
같은 타겟이 배열 내에 여러개 존재한다면 탐색 순서에 따라 결과가 달라질 수 있음

## 동작
n개의 데이터가 담긴 배열 arr을 반복문을 이용해 순회하며 target값과 비교
## 구현
임의의 배열 arr이 있을때 타겟 target을 찾는 소스코드  
존재하지 않다면 -1 반환  
#### Java
```java
// java file 'SequentialSearch.java'
public class SequentialSearch {
    public static void main(String[] args) {
        int[] arr = new int[]{1, 10, 5, 6, 7, 15};
        int target = 5;

        System.out.println(sequentialSearchFunc(arr, target));
        // it prints 2

        System.out.println(sequentialSearchFunc(arr, 550));
        // it prints -1
    }

    private static int sequentialSearchFunc(int arr[], int target) {
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] == target) return i;
        }
        return -1;
    }
}
```
#### C
```c
// C

#include <stdio.h>

int sequentialSearchFunc(int[], int, int);

int main()
{
    int arr[6] = { 1, 10, 5, 6, 7, 15 };
    int target = 5;

    printf("%d\n", sequentialSearchFunc(arr, sizeof(arr) / sizeof(arr[0]), target));
    // it prints 2
    printf("%d\n", sequentialSearchFunc(arr, sizeof(arr) / sizeof(arr[0]), 550));
    // it prints -1
    return 0;
}

int sequentialSearchFunc(int arr[], int arrLength, int target) {
    int i = 0;
    for(;i < arrLength; i++) {
        if(target == arr[i]) return i;
    }

    return -1;
}
```

## 시간복잡도

### 최선의 경우
한 번에 찾는 경우. O(1)

### 최약의 경우
n개의 데이터를 모두 순회하는 경우. O(n)

### 따라서 시간복잡도는
O(n)
