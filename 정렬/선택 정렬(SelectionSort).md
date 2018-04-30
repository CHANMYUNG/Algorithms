# 선택 정렬(Selection Sort)
## 설명
### 오름 차순 기준
가장 작은 수의 인덱스를 찾아 현재 위치 인덱스의 값과 Swap한다.<br>
한 사이클당 교환이 1회 이루어지므로 버블 정렬 보단 효율적이다.

## 동작

### 동작 예시
정수형 배열이 [5, 3, 2, 4, 1] `5개`의 원소를 가질 때 오름차순 정렬<br>

- 선형 탐색으로 가장 작은 값의 인덱스를 찾음 (인덱스 0 이상에서) 결과: 4<br>
  배열의 0번지의 값과 Swap<br>
  [`1`, 3, 2, 4, `5`]
- 선형 탐색으로 가장 작은 값의 인덱스를 찾음 (인덱스 1 이상에서) 결과: 2<br>
  배열의 1번지의 값과 Swap<br>
  [1, `2`, `3`, 4, 5]
- 선형 탐색으로 가장 작은 값의 인덱스를 찾음 (인덱스 2 이상에서) 결과: 2<br>
  배열의 2번지의 값과 Swap<br>
  [1, 2, `3`, 4, 5] // 불필요한 스왑 발생
- 선형 탐색으로 가장 작은 값의 인덱스를 찾음 (인덱스 3 이상에서) 결과: 3<br>
  배열의 3번지의 값과 Swap<br>
  [1, 2, 3, `4`, 5] // 불필요한 스왑 발생
- 선형 탐색으로 가장 작은 값의 인덱스를 찾음 (인덱스 4 이상에서) 결과: 4<br>
  배열의 4번지의 값과 Swap<br>
  [1, 2, 3, 4, `5`] // 불필요한 스왑 발생

때때로 **불필요한 교환이 일어남**을 알 수 있다.

## 시간 복잡도
O(n^2), 하지만 버블정렬보다는 훨씬 효율적이다.  

## 동작 영상
[![Select-sort with Gypsy folk dance](https://img.youtube.com/vi/Ns4TPTC8whw/0.jpg)](https://www.youtube.com/watch?v=Ns4TPTC8whw)

## 소스코드
```java
import java.util.Arrays;

public class SelectionSort {
    public static void main(String[] args) {
        int arr[] = {9, 3, 2, 1, 7, 8, 4, 10, 5, 6};

        int N = arr.length;

        for (int K = 0; K < N - 1; K++) {
            int minIdx = K;

            int j = K + 1;

            for (; j < N; j++) {
                if (arr[minIdx] > arr[j]) minIdx = j;
            }

            int temp = arr[K];
            arr[K] = arr[minIdx];
            arr[minIdx] = temp;
        }

        Arrays.stream(arr).forEach(System.out::println);
    }
}
```

## 번외
불필요한 스왑을 없애기 위해 값이 같은 경우 생략하는 코드를 추가할 수 있다.

### 소스코드
```java
import java.util.Arrays;

public class SelectionSortWithoutUselessSwap {
    public static void main(String[] args) {
        int arr[] = {9, 3, 2, 1, 7, 8, 4, 10, 5, 6};

        int N = arr.length;

        for (int K = 0; K < N - 1; K++) {
            int minIdx = K;

            int j = K + 1;

            for (; j < N; j++) {
                if (arr[minIdx] > arr[j]) minIdx = j;
            }

            if (arr[K] != arr[minIdx]) {
                int temp = arr[K];
                arr[K] = arr[minIdx];
                arr[minIdx] = temp;
            }
        }

        Arrays.stream(arr).forEach(System.out::println);
    }
}
```