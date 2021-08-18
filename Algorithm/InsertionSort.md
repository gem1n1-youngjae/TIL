## 삽입 정렬(Insertion Sort)

`Insertion Sort`는 `Selection Sort`와 유사하지만, 좀 더 효율적인 정렬 알고리즘이다.

`Insertion Sort`는 2번째 원소부터 시작하여 그 앞(왼쪽)의 원소들과 비교하여 삽입할 위치를 지정한 후, 원소를 뒤로 옮기고 지정된 자리에 자료를 삽입 하여 정렬하는 알고리즘이다.

최선의 경우 `O(N)`이라는 엄청나게 빠른 효율성을 가지고 있어, 다른 정렬 알고리즘의 일부로 사용될 만큼 좋은 정렬 알고리즘이다.

### 과정

1. 정렬은 2번째 위치(index)의 값을 `temp`에 저장한다.
2. `temp`와 이전에 있는 원소들과 비교하며 삽입한다.
3. '1'번으로 돌아가 다음 위치(index)의 값을 `temp`에 저장하고, 반복한다.

### Code (JavaScript)

```js
function InsertionSort(array) {
    for(int index = 1 ; index < array.length ; index++){
      int temp = arr[index];
      int prev = index - 1;
    while( (prev >= 0) && (array[prev] > temp) ) {
        array[prev+1] = array[prev];
        prev--;
    }
    array[prev + 1] = temp;
   }
  return array;
}
```

1. 첫 번째 원소 앞(왼쪽)에는 어떤 원소도 갖고 있지 않기 때문에, 두 번째 위치(index)부터 탐색을 시작합니다. `temp`에 임시로 해당 위치(index) 값을 저장하고, `prev`에는 해당 위치(index)의 이전 위치(index)를 저장한다.

2. 이전 위치(index)를 가리키는 `prev`가 음수가 되지 않고, 이전 위치(index)의 값이 '1'번에서 선택한 값보다 크다면, 서로 값을 교환해주고 `prev`를 더 이전 위치(index)를 가리키도록 한다.

3. '2'번에서 반복문이 끝나고 난 뒤, `prev`에는 현재 **`temp` 값보다 작은 값들 중 제일 큰 값의 위치(index)** 를 가리키게 됩니다. 따라서, (`prev+1`)에 `temp` 값을 삽입해준다.

### 장점

- 알고리즘이 단순하다.

- 대부분의 원소가 이미 정렬되어 있는 경우, 매우 효율적일 수 있다.

- 정렬하고자 하는 배열 안에서 교환하는 방식이므로, 다른 메모리 공간이 필요 없다.

- **안정 정렬(Stable Sort)** 이다.

- `Selection Sort`나 `Bubble Sort`과 같은 `O(n^2)` 알고리즘에 비교하여 상대적으로 빠르다.

### 단점

- 평균과 최악의 시간복잡도가 `O(n^2)`으로 비효율적이다.

- `Bubble Sort`와 `Selection Sort`와 마찬가지로, 배열의 길이가 길어질수록 비효율적이다.
