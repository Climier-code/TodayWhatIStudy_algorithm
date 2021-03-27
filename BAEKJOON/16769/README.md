# 백준 16769번 \_ Mixing Milk

> 시간을 줄일 수 있는 방법을 더 알아보자.

## [문제 보기](https://www.acmicpc.net/problem/16769)

## 놓친 것

    - 한줄로 짜면 동시에 작업이 이루어짐
    - max(), min()
    - 함수로 따로 빼서 짜면 시간이 훨씬 많이 걸린다...(?)

## 내가 짠 코드

```python
def pour(next_bt, current_m, next_m):
    if(current_m + next_m > next_bt):
        current_m = current_m + next_m - next_bt
        next_m = next_bt
        return current_m, next_m
    else:
        next_m = current_m + next_m
        current_m = 0
        return current_m, next_m


bt1, m1 = map(int,input().split())
bt2, m2 = map(int,input().split())
bt3, m3 = map(int,input().split())

for i in range(33):
    m1, m2 = pour(bt2,m1,m2)
    m2, m3 = pour(bt3,m2,m3)
    m3, m1 = pour(bt1,m3,m1)

m1, m2 = pour(bt2,m1,m2)

print(m1)
print(m2)
print(m3)
```

## 가장 적절한 코드

```python
C, M = list(), list()
for i in range(3):
    a,b = map(int, input().split())
    C.append(a)
    M.append(b)

for i in range(100):
    idx = i%3
    nxt = (idx+1) %3
    M[idx], M[nxt] = max(M[idx] -(C[nxt]-M[nxt]), 0), min(C[nxt], M[nxt]+M[idx])

for i in M:
    print(i)
```
