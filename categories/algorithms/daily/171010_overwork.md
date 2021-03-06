## 문제
야근 지수  
회사원인 수민이는 많은 일이 쌓여 있습니다. 수민이는 야근을 최소화하기 위해 남은 일의 작업량을 숫자로 메기고, 일에 대한 야근 지수를 줄이기로 결정했습니다. 야근 지수는 남은 일의 작업량을 제곱하여 더한 값을 의미합니다. 수민이는 1시간 동안 남은 일 중 하나를 골라 작업량 1만큼 처리할 수 있습니다. 수민이의 퇴근까지 남은 N 시간과 각 일에 대한 작업량이 있을 때, noOvertime 함수를 제작하여 수민이의 야근 지수를 최소화 한 결과를 출력해 주세요. 예를 들어, N=4 일 때, 남은 일의 작업량이 [4, 3, 3] 이라면 야근 지수를 최소화하기 위해 일을 한 결과는 [2, 2, 2]가 되고 야근 지수는 22 + 22 + 22 = 12가 되어 12를 반환해 줍니다.

---

## 풀이
* 로직
    * 남은 작업량이 n일 때 야근지수는 n^2이다.
    * 한시간을 투자하면 야근지수는 (n-1)^2이다.
    * 시간당 야근지수의 감소량 r = n^2 - (n^2 - 2n + 1) = 2n - 1.
    * r과 n은 비례하므로 매 시간마다 많이 남은 일부터 처리해야 한다는 결론 도출.

* 구현(python)
    1. 반복문(n회)을 만든다.
    1. max 함수로 works 에서 가장 큰 수를 찾는다.
    1. index 함수로 해당 수의 인덱스 넘버를 찾고, 1씩 감산한다.
    1. 반복문 밖에서 리스트 각 요소의 제곱의 합을 구하여 반환한다.

```python
def noOvertime(n, works):
    for i in range(n):
        works[works.index(max(works))] -= 1
    remain = sum([i ** 2 for i in works])
    return remain
```

> 매 반복마다 sort해서 works[0]만 1씩 감산하는 방법도 있다. 잘 읽히기는 그쪽이 나을 것 같다.
> 이 문제는 데일리 알고리즘을 시작하면서 열어봤을 땐 엄두가 안났었다. 쉬운 것 부터 풀어가다가 2주만에 다시 만났는데 순식간에 풀어서 신기하다. 컴퓨터적 사고보단 수리적 추론이 관건인건 함정(그때도 차분히 봤다면 풀었을 것).