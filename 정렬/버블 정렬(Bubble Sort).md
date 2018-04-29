# 버블 정렬(Bubble Sort)
## 설명
가장 직관적이고 대부분의 경우 가장 비효율적인 정렬 알고리즘 <br>
따라서 거의 쓰이지 않는다.

## 동작
구현에 따라 달라지지만 통상 가장 오른 원소부터 차례대로 자리를 찾아가게됨 <br>
자신과 자신의 다음 원소를 비교하고, Swap 여부를 결정<br>

### 동작 예시
정수형 배열이 [1, 2, 4, 2, 5, 7, 1, 3, 9, 8] `10개`의 원소를 가졌을 때 오름차순 정렬<br>

#### 시작: [1, 2, 4, 2, 5, 7, 1, 3, 9, 8]
- 1과 2 비교, Swap X<br>
  [**`1, 2`**, 4, 2, 5, 7, 1, 3, 9, 8]
- 2와 4 비교, Swap X<br>
  [1, **`2, 4`**, 2, 5, 7, 1, 3, 9, 8]
- 4와 2 비교, Swap O<br>
  [1, 2, **`2, 4`**, 5, 7, 1, 3, 9, 8]
- 4와 5 비교, Swap X<br>
  [1, 2, 2, **`4, 5`**, 7, 1, 3, 9, 8]
- 5와 7 비교, Swap X<br>
  [1, 2, 2, 4, **`5, 7`**, 1, 3, 9, 8]
- 7과 1 비교, Swap O<br>
  [1, 2, 2, 4, 5, **`1, 7`**, 3, 9, 8]
- 7과 3 비교, Swap O<br>
  [1, 2, 2, 4, 5, 1, **`3, 7`**, 9, 8]
- 7과 9 비교, Swap X<br>
  [1, 2, 2, 4, 5, 1, 3, **`7, 9`**, 8]
- 9와 8 비교, Swap O<br>
  [1, 2, 2, 4, 5, 1, 3, 7, **`8, 9`**]

이를 반복하는데, 원소의 개수가 `N`개면 사이클이 도는 횟수는 **(N - 1)**회, 사이클이 `K`번째라 하면 해당 사이클에서 일어나는 비교의 수는 **(N - K)**회<br>
**(N - K + 1)**번째의 자리에 알맞는 원소가 들어가게됨

### 동작 영상
[![Bubble-sort with Hungarian ("Csángó") folk dance](https://img.youtube.com/vi/lyZQPjUT5B4/0.jpg)](https://www.youtube.com/watch?v=lyZQPjUT5B4)

## 시간 복잡도
O(n^2)

## 소스코드
```java
import java.util.Arrays;

public class BubbleSort {
    public static void main(String[] args) {
        int[] arr = new int[]{1, 2, 4, 2, 5, 7, 1, 3, 9, 8};

        int N = arr.length;

        for (int K = 0; K < N - 1; K++) {
            for (int j = 0; j < N - 1 - K; j++) {
                if (arr[j] > arr[j + 1]) {
                    int temp = arr[j + 1];
                    arr[j + 1] = arr[j];
                    arr[j] = temp;
                }
            }
        }

        Arrays.stream(arr).forEach(System.out::println);
    }
}
```

## 번외
한 사이클에서 원소의 위치 변경이 일어나지 않는다면, 정렬이 이미 끝났다고 간주할 수 있음<br>
따라서 플래그를 두어 불필요한 사이클이 일어나지 않도록 방지할 수 있음<br>

### 소스코드
```java
import java.util.Arrays;

public class BubbleSortWithFlag {
    public static void main(String[] args) {
        int[] arr = new int[]{1, 2, 4, 2, 5, 7, 1, 3, 9, 8};

        int N = arr.length;

        for (int K = 0; K < N - 1; K++) {
            boolean flag = false;
            for (int j = 0; j < N - 1 - K; j++) {
                if (arr[j] > arr[j + 1]) {
                    int temp = arr[j + 1];
                    arr[j + 1] = arr[j];
                    arr[j] = temp;
                    flag = true;
                }
            }
            if (!flag) break;
        }

        Arrays.stream(arr).forEach(System.out::println);
    }
}
```
