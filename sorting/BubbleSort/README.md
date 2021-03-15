# BubbleSort(버블정렬)

- **개념**: 맨 첫번째 인덱스부터 그 뒷자리랑 비교하면서 앞이 크면 자리를 바꿔주는 형식.

- **특징**: 한 바퀴를 돌면 가장 큰 값이 맨 뒷자리로 위치됨.

- **코드**
```python
def bubblesort(data):
    for index in range(len(data) - 1):
        swap = False
        for index2 in range(len(data) - index - 1):
            if data[index2] > data[index2 + 1]:
                data[index2], data[index2 + 1] = data[index2 + 1], data[index2]
                swap = True
        
        if swap == False:
            break
    return data
```

- 시간복잡도 : O(n) _ 완전 정렬 < BubbleSort < O(n^2) _ 완전 반대
