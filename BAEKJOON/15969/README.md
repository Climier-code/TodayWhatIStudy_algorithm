# 백준 15969번 \_ 행복

## [문제 보기](https://www.acmicpc.net/problem/15969)

## 놓친 것

    - max, min을 생각 못함
    - 백준에서 python input에 대한 숙련도가 아직 낮음

## 내가 짠 코드

```python
N = map(int, input().split())
data = list(map(int, input().split()))

data.sort()

print(data[-1]-data[0])
```

## 가장 적절한 코드

```python
N, lst = input(), list(map(int, input().split()))

print(max(lst)- min(lst))
```
