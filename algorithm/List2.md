# 1.

- 중첩
- **부분집합**
- 이진 탐색
- 선택 정렬, selection algorithm
- **이차원 델타 검색**
- **비트 연산**
- 전치 행렬
- 완전 탐색

달팽이 문제 

```python
import sys
sys.stdin = open("input.txt", "r")

T = int(input())
for tc in range(1, T+1):
    N = 100
    i = 0
    j = 0
    k = 0
    MAX = 0
    totals = []
    res = 0
    arr = [list(map(int, input().split())) for i in range(N)]
    #행의 합
    for i in range(0, 100):
        for j in range(0,100):
            res += arr[i][j]
        totals.append(res)
    #열의 합
    for j in range(0, 100):
        for i in range(0,100):
            res += arr[i][j]
        totals.append(res)
    #대각선의 합
    totals.append(sum(arr[k][k]) for k in range(0,100))
    # print(totals)
    MAX = int(max(totals))
    print(MAX)
    
```

```python
 python swea_행렬의\ 합.py
Traceback (most recent call last):
  File "swea_행렬의 합.py", line 27, in <module>
    MAX = int(max(totals))
TypeError: '>' not supported between instances of 'generator' and 'int'
```

