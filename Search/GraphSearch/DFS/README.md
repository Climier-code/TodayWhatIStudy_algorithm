# DFS(Depth-First Search)

> 깊이 우선 탐색

- **개념**: 정점에서 자식들을 먼저 탐색하는 탐색

- **특징**

  - need_visit 스택와 visited 큐, 두 개의 큐를 생성

- **코드**

```python
def dfs(graph, start_node):
    visited, need_visit = list(), list()
    need_visit.append(start_node)

    while need_visit:
        node = need_visit.pop()
        if node not in visited:
            visited.append(node)
            need_visit.extend(graph[node])

    return visited
```

- **시간복잡도**: O(V + E) \_ 정점의 수: V, 간선의 수: E
