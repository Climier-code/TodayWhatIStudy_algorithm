# SelectionSort(선택정렬)

- **개념**: 주어진 데이터 중 최소값을 찾아 맨 앞과 교체하는 것을 반복

- **특징**: 정렬하는 중간에 다 됐다! 이럴 일은 잘 없음

- **코드**
```python
def selection_sort(data):
    for stand in range(len(data) - 1):
        lowest = stand
        for index in range(stand + 1, len(data)):
            if data[lowest] > data[index]:
                lowest = index
        data[lowest], data[stand] = data[stand], data[lowest]
    return data
```

- 시간복잡도 : SelectionSort = O(n^2) _ 비슷
