# 백준 17389번 \_ 보너스 점수

## [문제 보기](https://www.acmicpc.net/problem/17389)

## 놓친 것

    - enumerate
    - A, B = 0, 0

## 내가 짠 코드

```python
N = int(input())
data = str(input())

bo = 0
su = 0

for i in range(N):
    if data[i] == 'O':
        su += i + 1 + bo
        bo += 1
    else:
        bo = 0

print(su)
```

## 가장 적절한 코드

```python
N, S = input(), input()

score, bonus = 0, 0

for idx, OX in enumerate(S):
    if OX == 'O':
        #score, bonus = socre + idx+1+bonus, bonus+1

        score += idx+1+bonus
        bonus +=1
    else:
        bonus = 0
print(score)
```
