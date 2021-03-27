# 백준 1074번 \_ Z

> 재귀를 써야할 것은 알았으나 어떻게 써야할지 감이 안잡혔음

## [문제 보기](https://www.acmicpc.net/problem/1074)

## 놓친 것

    - 2차원 배열에 대한 이해
    - 재귀에 대한 이해

## 내가 짠 코드

```python

```

## 가장 적절한 코드

```python
def Z(sz,x,y):
    if sz==1:
        return 0
    sz //=2
    for i in range(2):
        for j in range(2):
            if x < sz*(i+1) and y < sz*(j+1):
                return (i*2+j)*sz*sz + Z(sz, x-sz*i, y-sz*j)



N, r, c = map(int, input().split())

print(Z(2**N,r,c))
```
