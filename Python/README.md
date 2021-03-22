# Algorithm with Python

> 알고리즘에서 써먹을 수 있는 파이썬 문법들

# 값

- `inf`: 무한대에 가까운 값
- `a, b, c, d = list(), 1, 0, dict()`: 이거 한줄로 표현 가능

## 반복문

- `range(stop)`: 0, 1, 2, 3, 4, 5, 6, 7, 8, 9
- `range(start, stop)`: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
- `range(start, stop, step)`: 0, 2, 4, 6, 8, 10, 12, 14, 16, 18
- **리스트에서 하나하나 가져옴**: `for a in list:`

## List

- **초기화**: `list = []`
- **값 추가**: `list.append(들어갈 값)`
- **list comprehension**

```python
# 일반적인 list에 넣는 for문 방식
list = []
for n in range(1,11):
    if(n % 3 == 0):
        list.append(n)

# list comprehension(이걸 잘 사용해보자)
list = [n for n in range(1, 11) if n % 3 == 0]
```

- **index**

  - `list[-1]`: 가장 마지막 인덱스
  - `list[0:]`: 처음부터 끝까지
  - `list[0:-1]`: 처음부터 마지막의 바로 앞까지
  - `list[1:3]`: 1번부터 2번까지

- `a, b = [1,2]` => `a = 1, b = 2`

- **리스트 연결**: `list3 = list1 + list2`

- **리스트 자체를 뒤에 추가**:`list.extend([4,5])`

- **지우기**: `del list[1]`

- **맨 끝 인덱스 꺼내기(Stack)**: `list.pop(-1)` -> list의 마지막 인덱스가 사라지고 그 부분은 사라지게 됨.

- **첫 인덱스 꺼내기(Queue)**: `list.pop(0)` ->list 0번 인덱스는 사라지고 뒤의 것이 자동으로 당겨져옴

- **list에 특정 값이 있는지 탐색**

  - `if a not in list:`

- **정렬**
  - 오름차순 정렬: `list.sort()`
  - 순서 반대로: `list.reverse()`
  - 위의 둘 동시에: `list.sort(reverse=True)`
  - 원래 리스트는 두고 새로운 리스트 리턴: `list2 = sorted(list1)` -`sorted(리스트, 기준, reverse=True)`

## Dictionary

> Key와 Value가 한 쌍으로 이루어진 형태

- **for & Dictionary**

  - `distances = {node: float('inf') for node in graph}`

- **빈 리스트로 초기화**: defaultdict 함수를 사용해서, key에 대한 value를 지정하지 않았을 시, 빈 리스트로 초기화하기

```python
from collections import defaultdict

list_dict = defaultdict(list)
print (list_dict['key1'])
```

## set(집합)

- `{}`
- 값만 존재하고 키는 존재 X
- `set()`을 통해 집합 생성
- **원소 추가**
  - 하나의 데이터 추가 : `set.add(100)`
  - 둘 이상의 데이터 추가: `set.update([3,4,5])`
- **원소 제거**
  - `set.remove(3)`
  - `set.discard(3)`
- **집합 복사**: `a = set.copy()`

### 연산

- **합집합**: `c = a.union(b)`
- **교집합**: `c = a.intersection(b)`
- **차집합**: `c = a.difference(b)`
- **대칭 차집합**: `c = a.symmetric_difference(b)`
- **부분집합의 여부 확인**
  - `a.issubset(b)` - 부분집합이면 True
  - `a.issuperset(b)` - 부분집합이면 False
- **교집합의 여부 확인**: `a.isdisjoint(b)`

## Class(객체 지향 프로그래밍)

- **선언**: 꼭 `__init__(self, ~~)` 로 선언 해줘야함

```python
#객체지향으로 링크드 리스트 구현
class Node:
    def __init__(self, data, next=None):
        self.data = data
        self.next = next

class NodeMgmt:
    def __init__(self, data):
        self.head = Node(data)

    def add(self, data):
        if self.head == '':
            self.head = Node(data)
        else:
            node = self.head
            while node.next:
                node = node.next
            node.next = Node(data)

    def desc(self):
        node = self.head
        while node:
            print (node.data)
            node = node.next
```

## Queue

> 기본적인 내장 함수로 queue가 있음

- **가져오기**: `import queue`

### Queue

- **객체 생성**: `data_queue = queue.Queue()`
- **값 넣기**: `data_queue.put(1)`
- **값 꺼내기**: `data_queue.get()`
- **큐 크기**: `data_queue.qsize()`

### Lifo Queue

- **Lifo 큐 객체 생성**: `data_queue = queue.LifoQueue()`

### PriorityQueue

- **우선순위 큐 객체 생성**: `data_queue = queue.PriorityQueue()`
- **값 넣기**: `data_queue.put((5, 1))`

## HeapQueue

> heap queue를 라이브러리를 이용해 사용 가능

- **가져오기**
  - `import heapqueue`
  - `import heapq`
  - `from heapq import *`
- **배열을 heap queue로 선언**: `heapq.heapity(queue)`
- **값 넣기**: `heapq.heappush(queue, [2, 'A'])`
- **값 꺼내기**: `heapq.heappop(queue)` \_ 우선순위가 낮은 순서대로 pop

## Stack

> 리스트로 push, pop 모두 가능

## Hash

> 내장된 함수들이 존재

- **해쉬 키 생성**: `hash_data = hash(data)`
