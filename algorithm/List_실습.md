# Today

-SW Expert - 파이썬문제해결 List1, solvingclub 과제

# 느낀 점

- d1부터 차근차근 다 풀어보자
- (전기버스) idea는 대부분 비슷, 구현의 문제
- 제한시간 정해서 고민해보고 안되면 구글링
- (Flatten) 문제를 잘 읽고 예외조건 주의
- python 복습! (.index() 첫 날 배운거라는데 기억이 안난다.)
- **어려운 걸 많이 새롭게 풀기보다는 주기적으로 풀었던 알고리즘을 다시 풀어보자.**

# 숫자카드_swea 4834

- counting sort

- 뒤에서 세기

  - range활용
  - 같은 값이라면 큰 값 호출

- 공백없는 숫자를 list로 만들기
  
  ```python
  numbers_int = list(map(int, list(input())))
  ```

# 전기버스_swea 

- 충전기가 없는 곳을 zero로 count하여 3이상이면 0 호출

# Flatten

`.index()` : list에서 ()값의 index를 알려준다. 

```python
while dump > 0:
        blocks[blocks.index(max(blocks))] -= 1
        blocks[blocks.index(min(blocks))] += 1
        dump -= 1
        if max(blocks) - min(blocks) <= 1:
            break
            
    res = max(blocks) - min(blocks)
```

# list comprehension

- 더 효율적이다.