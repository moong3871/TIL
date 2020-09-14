# range

step 안주고 range(N,0) 해도 돌아는 간다. 다만 for문 안돌고 멈추는듯 (아무것도 출력안돼)

거꾸로 출력하려면 step 필수 range(N, 0, -1)

# 함수와 return

<img src="C:%5CUsers%5Csunny%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20200829045419436.png" alt="image-20200829045419436" style="zoom:67%;" />

![image-20200829045323653](C:%5CUsers%5Csunny%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20200829045323653.png)



# 백준, 입력

https://leedakyeong.tistory.com/entry/Python-sysstdin

`import sys`하고 사용해야해

input()과 성질 비슷한듯

- 입력 string으로 받고
- list 하고 받으면 잘린 스트링 리스트로 들어감

```python
a = '12345'
list[map(int, a)] #=> [1, 2, 3, 4, 5]
					# 주의, list안씌우고 map 프린트하면 주소값 나옴
list[map(int, list(a))] # [1, 2, 3, 4, 5]
```

