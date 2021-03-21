# Dijkstra

> 다익스트라 알고리즘(최단 경로 알고리즘)

- **개념**: 하나의 정점에서 다른 모든 정점 간의 각각 가장 짧은 거리를 구하는 문제

- **특징**
  - BFS와 유사
  - 우선순위 큐(Max Heap) 쓰면 훨씬 빨라짐
  - 첫 정점을 기준으로 연결되어 있는 정점들을 추가해 가며, 최단 거리를 갱신하는 기법
- **순서**

  1. 초기화
     - 첫 정점을 기준으로 배열을 선언하여 첫 정점에서 각 정점까지의 거리를 저장
       - 초기에는 첫 정점의 거리는 0, 나머지는 무한대로 저장함 (inf 라고 표현함)
       - 우선순위 큐에 (첫 정점, 거리 0) 만 먼저 넣음
  2. 우선순위 큐에서 추출한 (A, 0) [노드, 첫 노드와의 거리] 를 기반으로 인접한 노드와의 거리 계산
  3. 우선순위 큐에서 (C, 1) [노드, 첫 노드와의 거리] 를 기반으로 인접한 노드와의 거리 계산¶
  4. 우선순위 큐에서 (D, 2) [노드, 첫 노드와의 거리] 를 기반으로 인접한 노드와의 거리 계산
  5. 우선순위 큐에서 (E, 5) [노드, 첫 노드와의 거리] 를 기반으로 인접한 노드와의 거리 계산
  6. 우선순위 큐에서 (B, 6), (F, 6) 를 순차적으로 추출해 각 노드 기반으로 인접한 노드와의 거리 계산 -> 안의 거리보다 큐에서 꺼낸 가중치가 더 크면 그냥 넘김(불필요한 계산 X)

- **장점**

  - 지금까지 발견된 가장 짧은 거리의 노드에 대해서 먼저 계산
  - 더 긴 거리로 계산된 루트에 대해서는 계산을 스킵할 수 있음

- **코드**

```python
#값 넣기
mygraph = {
    'A': {'B': 8, 'C': 1, 'D': 2},
    'B': {},
    'C': {'B': 5, 'D': 2},
    'D': {'E': 3, 'F': 5},
    'E': {'F': 1},
    'F': {'A': 5}
}

import heapq

def dijkstra(graph, start):
    # 초기화
    distances = {node: float('inf') for node in grap h}
    distances[start] = 0
    queue = []
    heapq.heappush(queue, [distances[start], start])

    while queue:
        current_distance, current_node = heapq.heappop(queue)

        #필요없는 계산 제거
        if distances[current_node] < current_distance:
            continue

        for adjacent, weight in graph[current_node].items():
            distance = current_distance + weight

            #가중치 업데이트
            if distance < distances[adjacent]:
                distances[adjacent] = distance
                heapq.heappush(queue, [distance, adjacent])

    return distances
```

- **최단경로출력**
  > 탐색할 그래프의 시작 정점과 다른 정점들간의 최단 거리 및 최단 경로 출력하기

```python
import heapq

# 탐색할 그래프와 시작 정점을 인수로 전달받습니다.
def dijkstra(graph, start, end):
    # 시작 정점에서 각 정점까지의 거리를 저장할 딕셔너리를 생성하고, 무한대(inf)로 초기화합니다.
    distances = {vertex: [float('inf'), start] for vertex in graph}

    # 그래프의 시작 정점의 거리는 0으로 초기화 해줌
    distances[start] = [0, start]

    # 모든 정점이 저장될 큐를 생성합니다.
    queue = []

    # 그래프의 시작 정점과 시작 정점의 거리(0)을 최소힙에 넣어줌
    heapq.heappush(queue, [distances[start][0], start])

    while queue:

        # 큐에서 정점을 하나씩 꺼내 인접한 정점들의 가중치를 모두 확인하여 업데이트합니다.
        current_distance, current_vertex = heapq.heappop(queue)

        # 더 짧은 경로가 있다면 무시한다.
        if distances[current_vertex][0] < current_distance:
            continue

        for adjacent, weight in graph[current_vertex].items():
            distance = current_distance + weight
            # 만약 시작 정점에서 인접 정점으로 바로 가는 것보다 현재 정점을 통해 가는 것이 더 가까울 경우에는
            if distance < distances[adjacent][0]:
                # 거리를 업데이트합니다.
                distances[adjacent] = [distance, current_vertex]
                heapq.heappush(queue, [distance, adjacent])

    path = end
    path_output = end + '->'
    while distances[path][1] != start:
        path_output += distances[path][1] + '->'
        path = distances[path][1]
    path_output += start
    print (path_output)
    return distances

# 방향 그래프
mygraph = {
    'A': {'B': 8, 'C': 1, 'D': 2},
    'B': {},
    'C': {'B': 5, 'D': 2},
    'D': {'E': 3, 'F': 5},
    'E': {'F': 1},
    'F': {'A': 5}
}

print(dijkstra(mygraph, 'A', 'F'))
```

- **시간복잡도**
  - O(E): 각 노드마다 인접한 간선들을 모두 검사하는 과정
  - O(E logE): 우선순위 큐에 노드/거리 정보를 넣고 삭제(pop)하는 과정
- **heap의 시간복잡도**
  - O(logn)
