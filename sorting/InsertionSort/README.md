# InsertionSort(삽입정렬)

- **개념**: 두 번째 인덱스의 값부터 뽑아서 뽑은 값이 앞이랑 비교하여 작을 때까지 반복하여 값을 교환하는 형식.

- **특징**: 하나하나 비교해야 함.

- **코드**
```python
def insertion_sort(data):
    for index in range(len(data) - 1):
        for index2 in range(index + 1, 0, -1):
            if data[index2] < data[index2 - 1]:
                data[index2], data[index2 - 1] = data[index2 - 1], data[index2]
            else:
                break
    return data
```

- 시간복잡도 : O(n) _ 완전 정렬 < InsertionSort < O(n^2) _ 완전 반대
