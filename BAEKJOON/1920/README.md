# 백준 1920번 \_ 수찾기

> 정석은 이진탐색 + 찾기-> 근데 왜 오류나?

## [문제 보기](https://www.acmicpc.net/problem/1920)

## 놓친 것

    - 일단 성공 X
    - Dictionary 사용
    - Dictionary comprehension
    - Dict.get(a,b) _ a = 찾을 값, b = 값이 없으면 출력

## 내가 짠 코드

```python
N = int(input())
A = list(map(int,input().split()))
M = int(input())
B = list(map(int,input().split()))


for i in B:
    if i not in A:
        print(0)
    else:
        print(1)

```

```python
def bns(lst, search):
    if(len(lst)==1 and search == lst[0]):
        return 1
    if(len(lst)==1 and search != lst[0]):
        return 0
    if len(lst)==0:
        return 0

    med = len(lst)//2
    if(search == lst[med]):
        return 1
    else:
        if(search > lst[med]):
            return bns(lst[med+1:],search)
        else:
            return bns(lst[:med],search)

N = int(input())
A = list(map(int,input().split()))
M = int(input())
B = list(map(int,input().split()))

A.sort()

for i in range(M):
    print(bns(A,B[i]))
```

## 가장 적절한 코드

```python
N, A = int(input()), {i: 1 for i in map(int, input().split())}

M = input()

for i in list(map(int, input().split())):
    print(A.get(i,0))
```
