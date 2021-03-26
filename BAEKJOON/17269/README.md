# 백준 17269번 \_ 이름궁합 테스트

## [문제 보기](https://www.acmicpc.net/problem/17269)

## 놓친 것

    - 문자열 + 문자열
    - list comprehension
    - +=
    - {}%.format

## 내가 짠 코드

```python
[N, M] = list(map(int, input().split()))
[A, B] = list(map(str, input().split()))

db = [3,2,1,2,4,3,1,3,1,1,3,1,3,2,1,2,2,2,1,2,1,1,1,2,2,1]

da = []

for i in range(min(N,M)):
    da.append(A[i])
    da.append(B[i])

if(N>M):
    for j in range(M,N):
        da.append(A[j])
elif(N<M):
    for j in range(N,M):
        da.append(B[j])

for l in range(N+M):
    da[l]= db[ord(da[l])-65]

k = N+M
while 1:
    if(k == 2):
        break
    for o in range(k-1):
        da[o] = (da[o]+da[o+1])%10
    k = k-1

if(da[0]!=0):
    print(str(da[0]*10+da[1])+'%')
else:
    print(str(da[1])+'%')

```

## 가장 적절한 코드

```python
N, M = map(int, input().split())
A, B = input().split()

alp = [3,2,1,2,4,3,1,3,1,1,3,1,3,2,1,2,2,2,1,2,1,1,1,2,2,1]

AB = ''
min_len = min(N,M)
for i in range(min_len):
    AB += A[i]+B[i]

AB += A[min_len:] + B[min_len:]

lst = [alp[ord(i)-ord('A')] for i in AB]

for i in range(N+M-2):
    for j in range(N+M-i-1):
        lst[j] += lst[j+1]

print("{}%".format(lst[0]%10*10 + lst[1]%10))

```
