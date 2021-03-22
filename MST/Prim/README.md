# Prim's algorithm

> 프림 알고리즘

- **개념**: 시작 정점을 선택한 후, 정점에 인접한 간선중 최소 간선으로 연결된 정점을 선택하고, 해당 정점에서 다시 최소 간선으로 연결된 정점을 선택하는 방식으로 최소 신장 트리를 확장해가는 방식

- **특징**

  - 탐욕 알고리즘을 기초로 함
  - 특정 정점에서 시작하여 그 중에서 가중치가 낮은 간선을 선택하여 노드 연결
  - 간선의 가중치를 간선리스트에 저장 후 작은 것을 선택해서 씀.

- **순서**

  1. 모든 간선 정보를 저장 (adjacent_edges)
  2. 임의의 정점을 선택, '연결된 노드 집합'에 삽입
  3. 선택된 정점에 연결된 간선들을 간선 리스트에 삽입
  4. 간선 리스트에서 최소 가중치를 가지는 간선부터 추출해서 사이클 체크하여 사이클 안되면 선택
  5. 추출한 간선은 간선 리스트에서 제거
  6. 간선 리스트에 더 이상의 간선이 없을 때까지 3-4번을 반복

- **코드**

```python
# 간선의 가중치와 노드 방향 넣기
myedges = [
    (7, 'A', 'B'), (5, 'A', 'D'),
    (8, 'B', 'C'), (9, 'B', 'D'), (7, 'B', 'E'),
    (5, 'C', 'E'),
    (7, 'D', 'E'), (6, 'D', 'F'),
    (8, 'E', 'F'), (9, 'E', 'G'),
    (11, 'F', 'G')
]
```

```python
from collections import defaultdict
from heapq import *

def prim(start_node, edges):
    mst = list()
    adjacent_edges = defaultdict(list)
    for weight, n1, n2 in edges:
        adjacent_edges[n1].append((weight, n1, n2))
        adjacent_edges[n2].append((weight, n2, n1))

    connected_nodes = set(start_node)
    candidate_edge_list = adjacent_edges[start_node]
    heapify(candidate_edge_list)

    while candidate_edge_list:
        weight, n1, n2 = heappop(candidate_edge_list)
        if n2 not in connected_nodes:
            connected_nodes.add(n2)
            mst.append((weight, n1, n2))

            for edge in adjacent_edges[n2]:
                if edge[2] not in connected_nodes:
                    heappush(candidate_edge_list, edge)

    return mst
```

- **시간복잡도**: O(E logE) \_ 최소 힙 구조 사용, 모든 간선에 대해서 반복(E = Edge 간선)

---

## 개선된 프림 알고리즘

> 간선이 아닌 노드 중심의 알고리즘

- **순서**
  1. 초기화 - 정점:key 구조를 만들어놓고, 특정 정점의 key값은 0, 이외의 정점들의 key값은 무한대로 놓음. 모든 정점:key 값은 우선순위 큐에 넣음
  2. 가장 key값이 적은 정점:key를 추출한 후(pop 하므로 해당 정점:key 정보는 우선순위 큐에서 삭제됨), (extract min 로직이라고 부름)
  3. 해당 정점의 인접한 정점들에 대해 key 값과 연결된 가중치 값을 비교하여 key값이 작으면 해당 정점:key 값을 갱신

```python
from heapdict import heapdict

def prim(graph, start):
    mst, keys, pi, total_weight = list(), heapdict(), dict(), 0
    for node in graph.keys():
        keys[node] = float('inf')
        pi[node] = None
    keys[start], pi[start] = 0, start

    while keys:
        current_node, current_key = keys.popitem()
        mst.append([pi[current_node], current_node, current_key])
        total_weight += current_key
        for adjacent, weight in mygraph[current_node].items():
            if adjacent in keys and weight < keys[adjacent]:
                keys[adjacent] = weight
                pi[adjacent] = current_node
    return mst, total_weight
```

```python
mygraph = {
    'A': {'B': 7, 'D': 5},
    'B': {'A': 7, 'D': 9, 'C': 8, 'E': 7},
    'C': {'B': 8, 'E': 5},
    'D': {'A': 5, 'B': 9, 'E': 7, 'F': 6},
    'E': {'B': 7, 'C': 5, 'D': 7, 'F': 8, 'G': 9},
    'F': {'D': 6, 'E': 8, 'G': 11},
    'G': {'E': 9, 'F': 11}
}
mst, total_weight = prim(mygraph, 'A')
print ('MST:', mst)
print ('Total Weight:', total_weight)
```

- **시간복잡도**: O(E logV) \_
  - O(V): 최초 key생성
  - O(VlogV): while문과 popitem
  - O(ElogV): while문 안의 for문 + key값의 변경 마다 heap구조 변경
  - O(V) + O(VlogV) + O(ElogV)인데 무조건 간선이 정점보다는 많으므로(E>V)이므로
