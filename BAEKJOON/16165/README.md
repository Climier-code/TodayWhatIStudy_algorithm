# 백준 16165번 \_ 걸그룹 마스터 준석이

## [문제 보기](https://www.acmicpc.net/problem/16165)

## 놓친 것

    - 일단 성공 X(생각한 방법은 똑같으나 뭔가 막힘)
    - 한 줄에 숫자 두 개면 맵으로 넣기(리스트 생성 X)
    - Dictionary를 2개 만들어 따로 저장 후 출력
    - 정렬 후 출력
    - 1 == True

## 내가 짠 코드

```python
N, M = map(int, input().split())

idol={}

for i in range(N):
    gname = str(input())
    K = int(input())
    names=[]
    for j in range(K):
        name = str(input())
        names.append(name)
    idol[gname]=names

for i in range(M):
    Qname = str(input())
    Qw = int(input())
    if(Qw == 1):
        for j in range(len(idol[Qname])):
            print(idol[Qname][i])
    else:
        for key, value in idol.items():
            if Qname in value:
                print(key)
```

## 가장 적절한 코드

```python
N, M = map(int, input().split())

team_mem, mem_team = {}, {}

for i in range(N):
    team_name,mem_num = input(), int(input())
    team_mem[team_name] = []
    for j in range(mem_num):
        name = input()
        team_mem[team_name].append(name)
        mem_team[name] = team_name

for i in range(M):
    name, q = input(), int(input())
    if q:
        print(mem_team[name])
    else:
        for mem in sorted(team_mem[name]):
            print(mem)
```
