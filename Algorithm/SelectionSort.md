## 선택 정렬(Selection Sort)
#Goal

`Selection Sort`는 `Bubble Sort`과 유사한 알고리즘으로, **해당 순서에 원소를 넣을 위치는 이미 정해져 있고, 어떤 원소를 넣을지 선택하는 알고리즘**이다.

`Selection Sort`와 `Insertion Sort`를 헷갈려하는 사람들이 종종 있는데, `Selection Sort`는 배열에서 **해당 자리를 선택하고 그 자리에 오는 값을 찾는 것**이라고 생각하면 편하다.


### 과정
1. 주어진 배열 중에 최소값을 찾는다.
2. 그 값을 맨 앞에 위치한 값과 교체한다. (pass)
3. 맨 처음 위치를 뺀 나머지 배열을 같은 방법으로 교체한다.

### Code (JavaScript)

```js
function SelectionSort(array) {
  let min, temp;
  for (let i = 0; i < array.length; i++) {
    min = i;
    for (let j = i + 1; j < array.length; j++) {
      if (array[j] < array[min]) {
        min = j;
      }
    }
    temp = array[min];
    array[min] = array[i];
    array[i] = temp;
  }
  return array;
}
```

1. 우선, 위치를 선택해준다.

2. `i+1`번째 원소부터 선택한 위치의 값과 비교를 시작한다.

3. 오름차순이므로 현재 선택한 자리에 있는 값보다 순회하고 있는 값이 작다면, 위치를 갱신해준다.

4. '2'번 반복문이 끝난 뒤에는 `min`에 '1'번에서 선택한 위치에 들어가야하는 값의 위치를 갖고 있으므로 서로 교환해준다.

### 장점
- `Bubble sort`와 마찬가지로 알고리즘이 단순하다.

- 정렬을 위한 비교 횟수는 많지만, `Bubble Sort`에 비해 실제로 교환하는 횟수는 적기 때문에 많은 교환이 일어나야 하는 자료상태에서 비교적 효율적이다.

- `Bubble Sort`와 마찬가지로 정렬하고자 하는 배열 안에서 교환하는 방식이므로, 다른 메모리 공간을 필요로 하지 않는다


### 단점
- 시간복잡도가 `O(n^2)`으로, 비효율적이다.

- 불안정 정렬(`Unstable Sort`) 이다.