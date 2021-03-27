# 백준 9037번 \_ The candy war

> 왜 시간초과.. why..

## [문제 보기](https://www.acmicpc.net/problem/9037)

## 놓친 것

    - 보이는 문제를 쪼개고 더 쪼개자(분할정복)
    - set을 하면 중복이 사라진다.
    - 플로우는 비슷함. but 내꺼는 시간초과

## 내가 짠 코드

```python
def ev(data):
    if data%2:
        return int(data//2+1)
    else:
        return int(data//2)

N = int(input())

for i in range(N):
    count = 0
    fsh = 1
    cn = int(input())
    ci_update = list(map(int, input().split()))
    ci_half=ci_update

    for j in range(cn):
        if ci_update[j]%2:
            ci_update[j] += 1

    while fsh:
        if max(ci_update)== min(ci_update):
            print(count)
            fsh = 0
        for j in range(cn):
            ci_half[j] = ev(ci_update[j])
        for k in range(cn):
            ci_update[k] = ev(ci_update[k]) + ci_half[k-1]
        count += 1
```

## 가장 적절한 코드

```python
def check(N, candy):
    for i in range(N):
        if candy[i] %2 ==1:
            candy[i] += 1
    return len(set(candy)) ==1

def teacher(N, candy):
    tmp_lst = [0 for i in range(N)]
    for idx in range(N):
        if candy[idx] % 2:
            candy[idx] +=1
        candy[idx] //= 2
        tmp_lst[(idx+1)%N] = candy[idx]

    for idx in range(N):
        candy[idx] += tmp_lst[idx]

    return candy



def process():
    N, candy = int(input()), list(map(int,input().split()))
    cnt = 0
    while not check(N,candy):
        cnt += 1
        candy = teacher(N,candy)
    print(cnt)


for i in range(int(input())):
    process()
```
