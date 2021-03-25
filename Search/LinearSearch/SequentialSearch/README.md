# Sequential Search

> 순차탐색

- **개념**: 앞에서부터 하나하나 비교해가며 탐색

- **코드**

```python
def sequencial(data_list, search_data):
    for index in range(len(data_list)):
        if data_list[index] == search_data:
            return index
    return -1
```

- **시간복잡도**: O(n)
