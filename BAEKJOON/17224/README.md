# 백준 17224번 \_ APC는 왜 서브태스크 대회가 되었을까?

## [문제 보기](https://www.acmicpc.net/problem/17224)

## 놓친 것

    - 성공( but 100점 만점은 140점)
    - 한 줄에 숫자 두 개면 맵으로 넣기(리스트 생성 X)
    - easy, hard 따로 계산 _ 더 명확하게 진행

## 내가 짠 코드

```python
[N, L, K] = list(map(int, input().split()))

count = 0

solve = 0

for i in range(N):
    if(count==K):
        break

    qs=list(map(int,input().split()))

    if(qs[1]<=L):
        solve += 140
    elif(qs[0]<=L):
        solve += 100

print(solve)
```

## 가장 적절한 코드

```python
N, L, K = map(int, input().split())

easy, hard = 0, 0

for i in range(N):
    sub1, sub2 = map(int,input().split())
    if sub2<= L:
        hard += 1
    elif sub1 <= L:
        easy += 1
ans = min(hard, K) *140

if hard < K:
    ans += min(K-hard, easy)*100
print(ans)
```
