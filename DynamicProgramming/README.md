# Dynamic Programming(DP)
> 동적계획법(DP)

- **상향식 접근법**: **작은**  문제들을 해결한 후, 그것의 답을 활용해서, 이전보다 큰 부분의 문제를 해결하여 전체 문제를 해결하는 알고리즘

- **특징**: Memoization
    - 이전에 계산한 값을 저장하고 이후에 그 값을 활용하면서 다시 계산하지 않도록 하여 전체 실행 속도를 빠르게 하는 기술
    - 부분 문제의 해답을 저장해서 재활용하는 최적화 기법으로 사용

- **코드 예시**: 피보나치 수열
```python
#재귀 호출
def fibo(num):
    if num <= 1:
        return num
    return fibo(num - 1) + fibo(num - 2)
```
```python
#DP
def fibo_dp(num):
    cache = [ 0 for index in range(num + 1)]
    cache[0] = 0
    cache[1] = 1
    
    for index in range(2, num + 1):
        cache[index] = cache[index - 1] + cache[index - 2]
    return cache[num]
```

- **시간복잡도**: 크기가 작을 때는 재귀와 비슷 _ O(n), 클 경우 DP가 훨씬 빠름(feat. Memoization)
