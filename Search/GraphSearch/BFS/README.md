# BFS(Breadth-First Search)

> 너비 우선 탐색

- **개념**: 정점에서 레벨이 같은 노드가 있으면 그 노드들을 먼저 탐색하고 내려가는 방식

- **특징**

  - need_visit 큐와 visited 큐, 두 개의 큐를 생성

- **코드**

```python
def bfs(graph, start_node):
    visited = list()
    need_visit = list()

    need_visit.append(start_node)

    while need_visit:
        node = need_visit.pop(0)
        if node not in visited:
            visited.append(node)
            need_visit.extend(graph[node])

    return visited
```

- **시간복잡도**: O(V + E) \_ 정점의 수: V, 간선의 수: E
