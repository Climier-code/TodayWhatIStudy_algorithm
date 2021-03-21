# GraphSearch

> 그래프에서 탐색을 해보자

## 그래프란?

- 정점또는 노드 사이를 간선으로 표현한 형태

### 그래프 관련 용어

- 노드: 정점
- 간선: 정점들을 연결한 선
- 인접 정점: 간선으로 연결된 정점
- 사이클: 시작정점과 종료정점이 일치하는 경우
- 단순경로: 중복된 정점이 없이 한 길로 연결된 경로
- 경로 길이: 경로를 구성하기 위해 사용된 간선의 수

### 그래프의 종류

- 무방향 그래프(Undirected Graph)
  - 방향이 없음
  - 양방향으로 이동가능
  - (A,B) == (B,A)
- 방향 그래프(Directed Graph)
  - 간선에 방향이 있음
  - 한쪽 방향으로만 이동가능
  - <A,B> != <B,A>
  - A->B != B->A
- 가중치 그래프(Weighted Graph or Network)
  - 간선에 가중치가 있어 간선간의 우선순위를 결정할 수 있는 그래프

### Graph Code

- 파이썬의 Dictionary & List로 구현 가능

```python
graph = dict()

graph['A'] = ['B', 'C']
graph['B'] = ['A', 'D']
graph['C'] = ['A', 'G', 'H', 'I']
graph['D'] = ['B', 'E', 'F']
graph['E'] = ['D']
graph['F'] = ['D']
graph['G'] = ['C']
graph['H'] = ['C']
graph['I'] = ['C', 'J']
graph['J'] = ['I']
```

### 트리 VS 그래프

- 트리
  - 그래프의 특별한 종류
  - 방향, 비순환 그래프
  - 최상위 노드 존재
  - 부모 자식 관계 존재
- 그래프
  - 루트 노드 존재 X
  - 부모 자식 관계 존재 X

### 그래프의 알고리즘 종류

- [DFS](DFS)
- [BFS](BFS)
- [ShortestPath](ShortestPath)
