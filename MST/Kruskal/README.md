# Kruskal's algorithm

> 크루스칼 알고리즘

- **개념**: Greedy Method를 이용하여 Spanning Tree의 모든 정점을 최소 비용으로 연결하는 최적 해답을 구하는 것

- **특징**

  - Greedy Algorithm을 베이스로 함
  - Union-Find Algorithm을 이용

- **순서**
  1. 모든 정점을 독립적인 집합으로 만듬
  2. 모든 간선을 가중치를 기준으로 정렬하고, 비용이 작은 간선부터 양 끝의 두 정점을 비교한다.
  3. 두 정점의 최상위 정점을 확인하고, 서로 다를 경우 두 정점을 연결한다.(사이클을 생기지 않게 해야함)

## Union-Find Algorithm

- **목적**
  - 연결된 노드를 찾거나, 노드들을 연결하거나 합칠 때 사용
  - 서로소인 집합을 찾을 때 사용
  - Kruskal에서 서로다른 집합의 노드들을 합쳐 사이클이 생기지 않게 함(합치는 노드집합에 같은 노드가 있으면 사이클이 생기기 때문)
- **순서**

  1. n 개의 원소가 개별 집합으로 이뤄지도록 초기화
  2. 두 개별 집합을 하나의 집합으로 합침, 두 트리를 하나의 트리로 만듬
  3. 여러 노드가 존재할 때, 두 개의 노드를 선택해서, 현재 두 노드가 서로 같은 그래프에 속하는지 판별하기 위해, 각 그룹의 최상단 원소 (즉, 루트 노드)를 확인

- 최악의 경우 링크드리스트의 형태로 한 쪽으로 길게 늘어질 수 있음
  > Union-by-rank, Path compression를 이용하여 해결 가능

### Union-by-rank

> 각 트리의 rank(높이)를 기억해두고 붙이는 작업

- 만약 두 트리의 높이가 다르면 높이가 큰 트리에 작은 트리를 붙임(큰 트리의 루트노드를 작은트리의 루트노드로 되게 함)

- 같으면 한 트리의 높이를 1 증가시켜 붙여줌
- **장점**: 시간복잡도 O(N)->O(logN)

### Path compression

> 한줄로 쭉 연결된 노드를 하나의 루트노드에서 자식노드로 모두 바꾸는 방법

- Find를 한번 실행하면 루트노드를 바로 알 수 있음(이전에는 여러번 타고 가야함)
- **장점**: 시간복잡도를 거의 O(1)로 맞출 수 있음

---

## **Kurskal Code**

```python
# 정점 분리 및 양방향으로 모든 간선 다 적기(Dicitonary)
mygraph = {
    'vertices': ['A', 'B', 'C', 'D', 'E', 'F', 'G'],
    'edges': [
        (7, 'A', 'B'),
        (5, 'A', 'D'),
        (7, 'B', 'A'),
        (8, 'B', 'C'),
        (9, 'B', 'D'),
        (7, 'B', 'E'),
        (8, 'C', 'B'),
        (5, 'C', 'E'),
        (5, 'D', 'A'),
        (9, 'D', 'B'),
        (7, 'D', 'E'),
        (6, 'D', 'F'),
        (7, 'E', 'B'),
        (5, 'E', 'C'),
        (7, 'E', 'D'),
        (8, 'E', 'F'),
        (9, 'E', 'G'),
        (6, 'F', 'D'),
        (8, 'F', 'E'),
        (11, 'F', 'G'),
        (9, 'G', 'E'),
        (11, 'G', 'F')
    ]
}
```

```python
parent = dict()
rank = dict()

def find(node):
    # path compression 기법
    if parent[node] != node:
        parent[node] = find(parent[node])
    return parent[node]


def union(node_v, node_u):
    root1 = find(node_v)
    root2 = find(node_u)

    # union-by-rank 기법
    if rank[root1] > rank[root2]:
        parent[root2] = root1
    else:
        parent[root1] = root2
        if rank[root1] == rank[root2]:
            rank[root2] += 1


def make_set(node):
    parent[node] = node
    rank[node] = 0

def kruskal(graph):
    mst = list()

    # 1. 초기화
    for node in graph['vertices']:
        make_set(node)

    # 2. 간선 weight 기반 sorting
    edges = graph['edges']
    edges.sort()

    # 3. 간선 연결 (사이클 없는)
    for edge in edges:
        weight, node_v, node_u = edge
        if find(node_v) != find(node_u):
            union(node_v, node_u)
            mst.append(edge)

    return mst
```

## 시간복잡도

- O(ElogE) \_ quick sort, union-by-rank, path compression 기법 모두 사용시
