# MergeSort (합병 정렬)

> 하나의 리스트를 두 개의 균등한 크기로 분할하고 분할된 부분 리스트를 정렬한 다음, 두 개의 정렬된 부분 리스트를 합하여 전체가 정렬된 리스트가 되게 하는 방법
- 퀵 정렬과 함께 많이 언급되는 빠른 정렬로, 안정 정렬에 속한다. 

## 합병 정렬 알고리즘의 특징
- 단점
    - 레코드를 배열(Array)로 구성하면 임시 배열이 필요하다. -> 제자리 정렬이 아니게 된다.
- 장점
    - 안정 정렬에 속한다.
        - 따라서 데이터의 분포에 영향을 덜 받는다, 즉 입력 데이터가 무엇이든 정렬되는 시간은 비슷하다.
    - 레코드가 LinkedList로 구성된 경우 효율적이다.
        - 합병 정렬은 순차적으로 정렬을 진행하기 때문에 효율적인 것
        - 퀵 정렬은 순차 접근이 아닌 랜덤 접근 방식이기 때문에 LinkedList가 비효율적이다.
    - 크기가 큰 레코드를 연결리스트를 사용하여 정렬하는 경우 효과적으로 사용할 수 있다. 

## 합병 정렬의 시간 복잡도
- O(NlogN)
- 평균, 최선, 최악의 시간복잡도 모두 NlogN이다.

## Java 코드
```java
private void solve() {
    int[] array = { 230, 10, 60, 550, 40, 220, 20 };
 
    mergeSort(array, 0, array.length - 1);
 
    for (int v : array) {
        System.out.println(v);
    }
}
 
public static void mergeSort(int[] array, int left, int right) {
    if (left < right) {
        int mid = (left + right) / 2;
 
        mergeSort(array, left, mid);
        mergeSort(array, mid + 1, right);
        merge(array, left, mid, right);
    }
}
 
public static void merge(int[] array, int left, int mid, int right) {
    int[] L = Arrays.copyOfRange(array, left, mid + 1);
    int[] R = Arrays.copyOfRange(array, mid + 1, right + 1);
 
    int i = 0, j = 0, k = left;
    int ll = L.length, rl = R.length;
 
    while (i < ll && j < rl) {
        if (L[i] <= R[j]) {
            array[k] = L[i++];
        } else {
            array[k] = R[j++];
        }
        k++;
    }
 
    while (i < ll) {
        array[k++] = L[i++];
    }
 
    while (j < rl) {
        array[k++] = R[j++];
    }
}

```

## 출처
- https://gmlwjd9405.github.io/2018/05/08/algorithm-merge-sort.html
- https://gyoogle.dev/blog/algorithm/Merge%20Sort.html

## 예상 질문
- 합병 정렬(merge sort)가 무엇인지 개념과 정렬 과정에 대해 설명해주세요.
- 합병 정렬에서 효율적으로 접근할 수 있는 자료구조가 무엇인지, 퀵 정렬과 비교하여 설명해주세요.
