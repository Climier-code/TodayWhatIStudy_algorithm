# Greedy Algorithm

> 탐욕 알고리즘

- **개념**: 최적의 해에 가까운 값을 구할 때 사용

- **특징**

  - 매 순간 최적이라고 생각되는 것을 계산
  - 반드시 최적의 해를 구할 수 있는 것은 아님 -> 미래를 고려하고 계산하는 것이 아닌 현재 상황에서 가장 최선인 것을 선택하기 때문
  - 문제에서 맞는 sort를 한 후 문제를 풀어나감

- **예시 문제**
  - 지불해야 하는 값이 4720원 일 때 1원 50원 100원, 500원 동전으로 동전의 수가 가장 적게 지불하시오.
    - 가장 큰 동전부터 최대한 지불해야 하는 값을 채우는 방식으로 구현 가능
    - 탐욕 알고리즘으로 매순간 최적이라고 생각되는 경우를 선택하면 됨

```python
coin_list = [1, 100, 50, 500]
print (coin_list)
coin_list.sort(reverse=True)
print (coin_list)

coin_list = [500, 100, 50, 1]

def min_coin_count(value, coin_list):
    total_coin_count = 0
    details = list()
    coin_list.sort(reverse=True)
    for coin in coin_list:
        coin_num = value // coin
        total_coin_count += coin_num
        value -= coin_num * coin
        details.append([coin, coin_num])
    return total_coin_count, details
```
