# LowerBound
## LowerBound란?
이진 트리 알고리즘의 확장  
데이터의 개수가 n개인 배열 arr이 주어졌을 때 배열 arr의 데이터 중 특정 값 target 이상인 첫 번쨰 데이터가 몇 번째 데이터인지(1부터 시작) 구하는 알고리즘

## 동작
변수명 | 뜻
---|---
mid | 현재 탐색범위의 중간 인덱스. (ex - 탐색 범위가 0~6이라면 (0+6) / 2값인 3)
target | 이 값 이상의 수가 처음으로 나오는 위치를 찾아야 함
arr | n개의 데이터가 들어가있는 배열
n | arr의 원소의 개수
left | 현재 검색 범위의 첫 번째 인덱스
right | 현재 검색 범위의 마지막 인덱스

- arr[mid - 1] < target, target <= arr[mid] 인 값 mid를 구하는것이 핵심
- arr[mid]와 target값을 비교, `arr[mid] >= target`이 성립한다면 (left ~ mid)로 탐색 범위 축소
- 반대로 `arr[mid] < target`이 성립한다면 (mid + 1 ~ right)로 탐색 범위 축소
- 위 과정 반복
- left == right이 성립하는 경우 범위를 좁히다 더이상 좁힐 수 없다(한 곳에 정착했다, 값을 찾았다)는 의미이므로 mid + 1을 리턴

## 구현
#### Java
```Java
// java 'LowerBound.java'

public class LowerBound {
    public static void main(String[] args) {
        // 오름차순 정렬되어있는 상태
        int[] arr = new int[]{ 1, 22, 333, 444, 555, 666, 777, 888 };
        int target = 999;

        int idx = lowerBoundFunc(arr, k, 0, 8);
        System.out.println(idx);
    }

    private static int lowerBoundFunc(int[] arr, int target, int first, int last) {
        int mid = (first + last) / 2;
        if (first == last) return mid + 1; // 몇 '반째' 수냐임. 번지가 아님

        if (arr[mid] >= target) return lowerBoundFunc(arr, target, first, mid);
        else return lowerBoundFunc(arr, target, mid + 1, last);
    }
}
```

## 시간복잡도
이진 탐색과 별반 다르지 않다.
