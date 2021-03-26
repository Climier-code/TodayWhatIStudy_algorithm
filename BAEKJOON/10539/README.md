# 백준 10539번\_ 수빈이와 수열

## [문제 보기](https://www.acmicpc.net/problem/10539)

## 놓친 것

    - 배열 복사 후 수정 VS 배열에 값 추가
    - 백준에서 python print에 대한 숙련도가 아직 낮음

## 내가 짠 코드

```python
N = int(input())
da = db = list(map(int, input().split()))

sum = 0

for i in range(1,N):
    sum += da[i-1]
    da[i] = (db[i]*(i+1)-sum)

for j in range(N):
    print(da[j], end=' ')
```

## 가장 적절한 코드

```python
N, B = int(input()), list(map(int, input().split()))

A = [B[0]]

for i in range(1,N):
    A.append(B[i]*(i+1)-sum(A))

for i in A:
    print(i, end=' ')
```
