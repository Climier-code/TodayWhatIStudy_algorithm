# 백준 2920번 \_ 음계

> 왜 시간초과.. why..

## [문제 보기](https://www.acmicpc.net/problem/2920)

## 놓친 것

    - input().split() VS input().split(' ')
    - 데이터의 직접적인 비교보단 상황을 저장할 변수 설정도 생각해야함

## 내가 짠 코드

```python
data = list(map(int, input().split()))

sdata = sorted(data)
rdata = sorted(data, reverse = True)
if(data == sdata):
    print("ascending")
elif(data == rdata):
    print("descending")
else:
    print("mixed")
```

## 가장 적절한 코드

```python
a = list(map(int, input().split(' ')))

ascending = True
descending = True

for i in range(1,8):
    if a[i] > a[i-1]:
        descending = False
    elif a[i] < a[i-1]:
        ascending = False

if ascending:
    print('ascending')
elif descending:
    print('descending')
else:
    print('mixed')
```
