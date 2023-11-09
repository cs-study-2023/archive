# 삽입정렬(Insertion Sort)

## 개념정리

### 정의

![삽입정렬](https://velog.velcdn.com/images%2Fdelmasong%2Fpost%2F9a836b65-dcf7-48d9-8d6c-0e6307704b43%2FinsertionSort.gif)

- 2번째 원소부터 시작해 그 앞(왼쪽)의 원소들과 비교해 삽입할 위치를 지정한 후, 원소를 뒤로 옮기고 지정된 자리에 자료를 삽입하여 정렬하는 알고리즘

### 시간복잡도: O(n^2)

- best인 경우에는(이미 미리 정렬되어있음) O(n)

### 공간복잡도: O(n)

### Process

- 정렬 2번째 위치(index)의 값을 temp에 저장한다.
- temp와 이전에 있는 원소들과 비교해 삽입해나간다.
- '1'번으로 돌아간 다음 위(index)값을 temp에 저장하고, 반복한다.

```java
void insertionSort(int[] arr) {
	for(int index = 1; index < arr.length; index++) {
		//1) 2번째 원소부터 시작해
		int temp = arr[index];
		int prev = index - 1;
		//2) 앞에 있는 원소들과 비교해서 삽입할 위치를 정하고
		while((prev >= 0) && arr[prev] > temp) {
			//3) 원소를 하나씩 뒤로 옮김
			arr[prev + 1] = arr[prev];
			prev--;
		}
		//4)지정된 자리에 원소 삽입
		arr[prev + 1] = temp;
	}
}
```

삽입 정렬이란 1)2번째 위치부터 loop를 돌며 2)앞의 원소(들)과 비교해서 삽입할 위치를 정하고 3)원소를 뒤로 옮기고 4)지정된 자리에 원소 삽입하며 정렬

### 장점

- 단순
- 이미 정렬이 많이 되어있는 경우는 효율적
- 메모리 공간을 별도로 필요로 하지 않음 => 제자리 정렬
- **안정 정렬**
  - 안정 정렬(Stable Sort)은 동일한 값을 가진 데이터들의 순서가 원래의 순서와 같이 유지되는 정렬
  - 예시
    - list=[1, 7, 3, 5, 4, 7, 9] 이 리스트를 정렬했을 때
    - (1) list=[1, 3, 4, 5, 7(1), 7(2), 9] - 안정 정렬
    - (2) list=[1, 3, 4, 5, 7(2), 7(1), 9] - 불안정 정렬
- 상대적으로 다른 O(n^2) 알고리즘(버블 정렬, 선택 정렬)보다 빠름

### 단점

- 시간 복잡도: O(n^2)
- 배열 길이가 길어질 수록 비효율적

## 예상 질문

- 삽입 정렬(Insertion Sort)에 대해 설명해주세요.

---

### 참고자료

[개발자 서류 / 면접 준비 #4 - 정렬 뽀시기](https://velog.io/@tjdud0123/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EC%84%9C%EB%A5%98-%EB%A9%B4%EC%A0%91-%EC%A4%80%EB%B9%84-4-%EC%A0%95%EB%A0%AC-%EB%BD%80%EC%8B%9C%EA%B8%B0)<br>
[신입 개발자 기술면접 질문 정리 - 알고리즘
](https://dev-coco.tistory.com/160)
