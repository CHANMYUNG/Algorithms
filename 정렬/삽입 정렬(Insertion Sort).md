# 삽입 정렬(Insertion Sort)
## 설명
### 오름차순의 경우
K번째 원소를 이전 원소와 비교하며 이전 원소가 K번째 원소보다 작을 때 까지 이전 원소를 다음 인덱스의 값으로 이동시킨다. <br>
그 후 그 자리에 K번째 원소를 끼워 넣는다.

## 동작
### 동작 예시
정수형 배열이 [5, 3, 2, 4, 1] `5개`의 원소를 가질 때 오름차순 정렬<br>
**인덱스는 1부터 시작 (이전 원소와 비교해야 하는데 0은 이전 원소가 없다.)** <br>

- 3과 5 비교, 밀어내기 O <br>
  [5, `5`, 2, 4, 1]
- 3을 0번지에 끼워 넣음 <br>
  [`3`, 5, 2, 4, 1]
- 2와 5 비교, 밀어내기 O <br>
  [3, 5, `5`, 4, 1]
- 2와 3 비교, 밀어내기 O<br>
  [3, `3`, 5, 4, 1]
- 2를 0번지에 끼워 넣음 <br>
  [`2`, 3, 5, 4, 1]

이를 반복

## 시간 복잡도
O(n^2)

### 동작 영상
[![Insert-sort with Romanian folk dance](https://img.youtube.com/vi/ROalU379l3U/0.jpg)](https://www.youtube.com/watch?v=ROalU379l3U)

## 소스코드
```java
import java.util.Arrays;

public class InsertionSort {
    public static void main(String[] args) {
        int arr[] = {9, 3, 2, 1, 0, 6, 8, 4, 7};
        int N = arr.length;

        for (int K = 1; K < N; K++) {
            int target = arr[K];

            int j = K - 1;

            while (j >= 0 && target < arr[j]) {
                arr[j + 1] = arr[j];
                j--;
            }

            arr[j + 1] = target;
        }

        Arrays.stream(arr).forEach(System.out::println);
    }
}
```