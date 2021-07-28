# Stack 1

## 목차

- **스택**
  - 특성
  - 구현
  - 응용
    - 괄호검사
    - function call
- ==재귀호출==
  - 팩토리얼
  - 피보나치
- Memoization
- DP
- ==**DFS**== 

---



## 스택

- 스택의 특성

  - 자료를 차곡차곡 쌓아 올린 형태의 자료구조
  - 스택에 저장된 자료는 선형 구조`(1:1의 관계)`를 갖는다. `앞뒤가 존재한다`
  - 후입선출 **Last In First Out**

- 스택의 구현

  - `자료구조`와 `연산`이 필요하다.

    - 자료구조 : 저장소

    - 연산

      - `push` 삽입: 저장소에 자료 저장

      - `pop` 삭제: 저장소에서 자료 꺼내기

        ​	선행작업: **저장소가 비어있는지 확인**

      - `isEmpty`: 스택이 공백인지 아닌지 확인

      - `peek` : top에 있는 item 확인 (확인만 한다. pop처럼 삭제하는거 아니다.

    ```python
    # 자료구조
    stack = []
    
    # 연산
    def push(item):
        stack.append(item)
        
    def pop():
        if len(stack) == 0: #stack이 비었는지 확인
            print("stack is empty")
            return
        else:
            return stack.pop()
    ```

    

  - 연산 알고리즘

    ```python
    # push
    # append 메서드, 리스트의 마지막에 데이터 삽입
    s.append(item)
    
    # pop
    # 스택이 비어있는지 확인
    if len(s) == 0:
        return
    else:
        return s.pop(-1) # pop이라는 삭제 method 존재
    					 # s의 (-1)idx, 즉 마지막 item을 삭제
    ```

    `s.pop([i]) `retrieves the item at *i* and also removes it from *s*

    

- 스택의 응용

  - 괄호검사

  - function call

    - 1. 함수 호출이 발생 

      2. 호출한 함수 수행에 필요한 정보를 스택 프레임에 저장

         (지역변수, 매개변수 및 수행 후 복귀할 주소 등의 정보)

      3. 시스템 스택에 삽입

    - 함수의 실행이 끝나면 

      1. 시스템 스택의 top 원소를 삭제하면서  **(즉, return 하면 스택에서 삭제)**

      2. 프레임에 저장되어 있던 복귀 주소를 확인하고 복귀 

         *(stack에서 사라지고 호출된 곳으로 돌아간다)*

    - 함수의 실행이 끝나면 공백상태이다.

      

## 재귀호출

- 재귀의 기본 2가지 part
  - basis : 종료 조건
  - inductive(유도): 반복

- 일반적인 호출방식보다 **크기를 줄이고 간단하게 작성가능**

- factorial 함수

  ```python
  # f(n) = n * f(n-1)
  def fact(n):
      if n == 1:  # basic
          return 1
      else:		# inductive(유도)
          return n * fact(n-1)
  ```

- 피보나치 수열

  ```python
  def fibo(n):
      if n < 2: # 기본파트: 멈추는 부분
          return n
      else:	  # 유도파트
          return fibo(n-1) + fibo(n-2)
  ```



## Memoization

- **이전에 계산한 값을 메모리에 저장**해서 매번 다시 계산하지 않도록 하여 전체적인 **실행속도를 빠르게** 하는 기술

- 재귀함수의 문제점: 엄청난 중복 호출 --> 이전에 계산한 값을 메모리에 저장함으로써 중복호출 방지

  - 피보나치 수열의 재귀함수`O(n^2)` 실행시간을 `O(n)`으로 줄일 수 있다.

    ```python
    # memo를 위한 배열을 할당, 모두 0으로 초기화
    # memo[0]을 0으로 memo[1]은 1로 초기화
    
    def fibo1(n):
        global memo
        if n >= 2 and len(memo) <= n :
            memo.append(fibo1(n-1) + fibo1(n-2))
        return memo[n]
    memo = [0, 1]
    ```

    

  

  

