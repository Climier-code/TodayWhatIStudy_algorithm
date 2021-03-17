# MergeSort(병합 정렬)

- **개념**: split(list를 절반으로 하나가 될 때까지 자름) + merge(다시 하나하나 뭉치면서 순서를 정렬해 나감) _ 토너먼트랑 비슷하다고 생각하면 편할 듯.

- **특징**
    - 분할정복(재귀호출): 나눈다, 계산한다. -> 반복
    - `split`과 `merge`, 두 개의 함수를 만들어야함

- **코드**
```python
# split
def mergesplit(data):
    if len(data) <= 1:
        return data
    medium = int(len(data) / 2)
    left = mergesplit(data[:medium])
    right = mergesplit(data[medium:])
    return merge(left, right)

# merge
def merge(left, right):
    merged = list()
    left_point, right_point = 0, 0
    
    # case1 - left/right 둘다 있을때
    while len(left) > left_point and len(right) > right_point:
        if left[left_point] > right[right_point]:
            merged.append(right[right_point])
            right_point += 1
        else:
            merged.append(left[left_point])
            left_point += 1

    # case2 - left 데이터가 없을 때
    while len(left) > left_point:
        merged.append(left[left_point])
        left_point += 1
        
    # case3 - right 데이터가 없을 때
    while len(right) > right_point:
        merged.append(right[right_point])
        right_point += 1
    
    return merged
```

- 시간복잡도: O(n log n) = O(n) _ `병합하는 각 단계의 시간복잡도`* O(log n) _ `만들어지는 단계의 갯수`