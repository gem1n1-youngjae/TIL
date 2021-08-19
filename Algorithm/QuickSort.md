## 퀵 정렬 (Quick Sort)

`Quick Sort`은 **분할 정복(divide and conquer) 방법** 을 통해 주어진 배열을 정렬한다.

>분할 정복(divide and conquer) 방법 : 문제를 작은 2개의 문제로 분리하고 각각을 해결한 다음, 결과를 모아서 원래의 문제를 해결하는 전략이다.

`Quick Sort`은 불안정 정렬에 속하며, 다른 원소와의 비교만으로 정렬을 수행하는 비교 정렬에 속한다. 또한 Merge Sort와 달리 `Quick Sort`는 배열을 비균등하게 분할한다.

### 과정

1. 배열 가운데서 하나의 원소를 고릅니다. 이렇게 고른 원소를 **피벗(pivot)** 이라고 한다.

2. 피벗 앞에는 피벗보다 값이 작은 모든 원소들이 오고, 피벗 뒤에는 피벗보다 값이 큰 모든 원소들이 오도록 피벗을 기준으로 배열을 둘로 나눈다. 이렇게 배열을 둘로 나누는 것을 **분할(Divide)** 이라고 한다. 분할을 마친 뒤에 피벗은 더 이상 움직이지 않는다.

3. 분할된 두 개의 작은 배열에 대해 재귀(Recursion)적으로 이 과정을 반복한다. 

### Code (JavaScript)

퀵 정렬은 다음의 단계들로 이루어진다.

- 정복 (`Conquer`)

  부분 배열을 정렬한다. 부분 배열의 크기가 충분히 작지 않으면 순환 호출을 이용하여 다시 분할 정복 방법을 적용한다.

```js
  function quickSort(array, left, right) {
    if(left >= right) return;

    let pivot = partition(); 
    
    quickSort(array, left, pivot-1);  
    quickSort(array, pivot+1, right);
}
```

- 분할 (`Divide`)

  입력 배열을 피벗을 기준으로 비균등하게 2개의 부분 배열 **(피벗을 중심으로 왼쪽 : 피벗보다 작은 요소들, 오른쪽 : 피벗보다 큰 요소들)** 로 분할한다.
  
```js
const swap = (array, front, back) => {
	let tmp = array[front];
	array[front] = array[back];
	array[back] = tmp;
}

function partition(array, left, right) {
    let pivot = array[left]; // 가장 왼쪽값을 피벗으로 설정
    let i = left
    let j = right;
      
    while(i < j) {
        while(pivot < array[j]) {
          j--;
        }
        while(i < j && pivot >= array[i]){
          i++;
        }
        swap(array, i, j);
    }
    array[left] = array[i];
    array[i] = pivot;
      
    return i;
}
```


### 장점

- 불필요한 데이터의 이동을 줄이고 먼 거리의 데이터를 교환할 뿐만 아니라, 한 번 결정된 피벗들이 추후 연산에서 제외되는 특성 때문에, 시간 복잡도가 `O(nlog₂n)`를 가지는 다른 정렬 알고리즘과 비교했을 때도 가장 빠르다.

- 정렬하고자 하는 배열 안에서 교환하는 방식이므로, 다른 메모리 공간을 필요로 하지 않는다. 

### 단점

- **`불안정 정렬(Unstable Sort)`** 이다.
- 정렬된 배열에 대해서는 `Quick Sort`의 불균형 분할에 의해 오히려 수행시간이 더 많이 걸린다.