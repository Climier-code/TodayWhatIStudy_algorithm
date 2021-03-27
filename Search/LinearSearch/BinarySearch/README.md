# BinarySearch

> 이진탐색

- **개념**: 탐색할 자료를 둘로 나누어 해당 데이터가 있을만한 곳을 탐색

- **특징**

  - 정렬이 된 상태에서 사용을 해야함.
  - 분할 정복 알고리즘을 이용
  - Divide: 리스트를 두 개로 나눔
  - Conquer: 검색할 숫자가 크고 작음에 따라 앞 부분 서브리스트와 뒷 부분 서브 리스트를 선택하여 탐색

- **코드**

```python
def binary_search(data, search):
    print (data)
    if len(data) == 1 and search == data[0]:
        return True
    if len(data) == 1 and search != data[0]:
        return False
    if len(data) == 0:
        return False

    medium = len(data) // 2
    if search == data[medium]:
        return True
    else:
        if search > data[medium]:
            return binary_search(data[medium+1:], search)
        else:
            return binary_search(data[:medium], search)
```

- **시간복잡도**: O(log n) \_ n개의 리스트를 매번 2로 나누어 1이 될 때까지 비교연산을 함.
