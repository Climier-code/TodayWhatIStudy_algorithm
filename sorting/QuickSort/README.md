# QuickSort(퀵 정렬)

- **개념**: 기준점(pivot)을 정해서, 기준점보다 작은 것은 왼쪽으로, 그보다 큰 데이터는 오른쪽으로 모으는 함수를 끝까지 호출하여 반복 후 리턴하는 정렬.

- **특징**
    - 정렬 알고리즘의 끝판왕
    - **분할 정복(웬만하면 전부 재귀호출)**: 기준점을 정하고 크기에 따라 왼쪽 or 오른쪽으로 분할하는 것을 반복
    - 정렬 알고리즘 중에서 가장 많이 씀

- **코드**
```python
#일반
def qsort(data):
    if len(data) <= 1:
        return data
    
    left, right = list(), list()
    pivot = data[0]
    
    for index in range(1, len(data)):
        if pivot > data[index]:
            left.append(data[index])
        else:
            right.append(data[index])
    
    return qsort(left) + [pivot] + qsort(right)
```
```python
#list comprehension사용
def qsort(data):
    if len(data) <= 1:
        return data
    
    pivot = data[0]

    left = [ item for item in data[1:] if pivot > item ]
    right = [ item for item in data[1:] if pivot <= item ]
    
    return qsort(left) + [pivot] + qsort(right)
```
- **시간복잡도**: 평균적으로 O(n log n), 최악의 경우는 O(n^2)