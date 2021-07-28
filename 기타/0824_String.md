# 문자열(string)

- 영어, 한글, 라이브러리 어떻게 표현할건지
  - 라이브러리가 어떻게 구현되는지 살펴봐야 한다.
- 목차
  - 문자열
  - 패턴 매칭 (키워드, 패턴, 염기서열)
    - **brute force**
    - KMP
    - 보이어-무어
  - 문자열 암호화
  - 문자열 압축
  - 실습 1,2

​	

## 문자의 표현

### 컴퓨터에서의 문자표현

- 글자 A를 메모리에 저장하는 방법
  - 메모리는 숫자만을 저장할 수 있다
  - 각 문자에 대해서 대응되는 숫자를 정해 놓고 이것을 메모리에 저장하는 방법이 사용
- 영어가 대소문자 합쳐서 52, 6비트(64가지)면 모두 표현할 수 있다.
  - 7bit: ASCII (ASCII코드의 첫번째는 null)
- 문자 인코딩 표준: ASCII 
  - 7bit 인코딩으로 128문자를 표현하며 33개의 출력 불가능한 제어문자, 공백을 비롯한 95개의 출력 가능한 문자들로 구성
  - Byte = 8bit(bit의 단위는 0과 1) = 영문자 한 자를 나타내는 단위
    - if 100byte -> 영문자 100자
    - 하지만 ASCII는 **7bit**, 0~127문자, parity bit: 에러체크

==> **영문자는 7bit짜리 ASCII 코드를 사용**

- 확장아스키는 표준 문자 이외의 악센트 문자, 도형 문자, 특수 문자, 특수 기호 등 부가적인 문자를 추가할 수 있게했다. ==> 표준이 아니다. 지금은 안쓴다.



- 영어 외에도 다국어 처리를 위해 마련한 표준: **유니코드**(완성형)

- 유니코드도 Character Set으로 분류된다.

  - 유니코드를 저장하는 변수의 크기를 정하지 않음 (2, 4)
  - 바이트 순서에 대해서 표준화하지 못했음
    - big-endian, little-endian
      - 큰 단위가 앞에 (01, 02, 03, 04) : big-endian
  - 즉, 파일 인식 시 이 파일이 UCS-2, UCS-4인지 인식하고 각 경우를 구분해서 모두 다르게 구현해야 하는 문제 발생
  - ==> 유니코드의 **외부 인코딩**이 필요
  - **유니코드 인코딩**(UTF: Unicode Transformation Format)
    - **UTF-8** (web, **python**) 
    - UTF-16 (windows, java) 2개 or 4개짜리
    - UTF-32 (unix) 무조건 4개짜리

- 문자열의 분류

  - 고정 길이 / 가변 길이
  - 가변 길이 - length controlled(java-class로 지원) / delimited(C-type, 구분자(\0)로 구분)
    - C: char ary[]={'a', 'b', '\0'} 또는 char ary[] = "ab" 로 저장

- **Python에서의 문자열 처리**

  - char 타입 없음 ( 다 string(문자열)으로 취급)
    - 'ABC'와 "ABC" 동일
  - 문자열 기호
    - `+` 연결: `문자열 + 문자열` 이어 붙여주는 역할
    - `*`반복: `문자열 * 수` 수만큼 문자열이 반복
  - 문자열은 시퀀스 자료형으로 분류, **인덱스**로 접근 가능, 슬라이싱 연산 사용 가능
  - 제공되는 메소드
    - replace(), split(), isalpha(), find()
  - **문자열은 튜플과 같이 요소값을 변경할 수 없음(immutable)**
    - str = "ABC", str[0] = "F" 처럼 값을 부분적으로 바꿀 수 없다.

- C와 Java의 String 처리의 기본적인 차이점

  - C는 아스키 코드로 저장
    - 한글을 2자로 저장, 유니코드를 사용하는 python과 java는 한글을 1자로 저장

  

## 문자열 뒤집기

- 2가지

  - **자기 문자열에서 뒤집는 방법** 
  - 새로운 빈 문자열을 만들어 소스의 뒤에서부터 읽어서 타겟에 쓰는 방법

- 자기 문자열 이용

  - swap을 위함 임시 변수가 필요(python은 필요X), 반복 수행을 문자열 길이의 반만 수행

- #### 연습문제1

  - C에서는 자기 문자열로 구현

  - java에서는 StringBuffer 클래스의 reverse()메소드 이용

  - Python은 Reverse 함수 혹은 slice notation을 이용 `s[::-1`]

     `[::-1]` 마지막 index가 -1, 첫번째 인덱스로 오면서 -1씩 (음수 인덱스)

    - 자기 문자열로 할 경우

      - str[0, str[8]] = str[8], str[0] but immutable이여서 안돼. 따라서 리스트로 바꿔주기

      1. str을 list로 바꾸기
      2. list에서 swap
      3. list를 str로 바꿔주기

      ```python
      #algorithm 문자열 자기 문자열로 뒤집기
      for i in range(len(str)):
          arr = list(str[i])
      for j in range(len(arr)/2):
          arr[j], arr[len(arr)-j] = arr[len(arr)-j], arr[j]
      str = "".join(arr)    
      ```

      ```python
      def str_rev(str): #여기 str은 지역변수, 아래 reverse의 str과 다르다
          # str -> List
          arr = list(str)
          # swap
          for i in range(len(arr//2)): #/하면 실수형 출력 ex: 10 / 2 = 5.0
              arr[i], arr[len(arr)- 1 - i] = arr[len(arr) - 1 - i], arr[i]
          # List -> str
          str = "".join(arr)
          return str
      
      str = "algorithm"
      str1 = str_reverse(str)
      print(str1)
      ```

      ```python
      # 온라인 코칭
      for i in range(len(str)-1, -1, -1):
          print(str1[i], end="")
          
      str2 = str1[::-1]
      
      str3 = reversed(str1)
      print(''.join(str3))
      
      n=len(str1)//2
      str4 = list(str1)
      for i in range(n):
          str4[i], str[-1-i] = str4[-1-i],str4[i]
      print(''.join(str4))
      ```

      













## 문자열 비교

- c strcmp() 함수를 제공
- 파이썬에서는 ==연산자와 is 연산자를 제공한다.
  - ==연산자는 내부적으로 특수 메서드 `_eq_()`를 호출

- `strcmp`



### 문자열 숫자를 정수로 표현하기

repr로 출력하면 " "로 감싸져서 표현

- atio() : array to integer

  | 1    | 2    | 3    |
  | ---- | ---- | ---- |
  |      |      |      |

  을 123으로! 

  **`value = (value * 10) + digit `**

  

- 

### 문자열 교체하기

replace를 사용하여 보관했다가 복사, 붙여넣기

```python
str1 = "abc 1, 2, ABC"
str1 = str1.replace("1, 2", "one, two")
print(str1)

```

#### 연습문제 2

- str()함수를 사용하지 않고, itoa()를 구현해라.

  - 양의 정수를 입력 받아 문자열로 변환하는 함수
  - 입력 값: 변환할 정수 값, 변환된 문자열을 저장할 문자배열
  - 반환 값: 없음
  - 음수를 변환할 때는 어떤 고려 사항이 필요한가요?

  ```python
  # 라이브
  def itoa(num):
      x = num # 몫
      y = 0 # 나머지
      arr = []
      while x: # x != 0인 동안
          y = x % 10
          x = x // 10 # x //= 10과 동일
         # arr.append(chr(y + ord('0'))
      	arr.append(y)
      arr.reverse()
      # str = "".join(arr)
      return str
  ```

  ```python
  # 온라인 코칭 itoa: int형을 문자열로 전환
  def itoa(num):
      line = ''
      tmp = num
      while tmp > 0:
          number = tmp % 10
          line += chr(number + ord('0'))
          tmp // 10
  
      return line
  
  line = itoa(1234)
  print(type(line),line)
  ```

  ```python
  # 온라인 코칭 atoi: 문자열을 int형으로 전환
  def atoi(line):
      num = 0
      for i in range(len(line)):
          num *= 10 # 자릿수를 맞출 수 있다. 1 -> 10 + 2 -> 120 + 3 -> 1230 + 4
          num += ord(line[i]) - ord('0') # 숫자의 아스키코드 - 0의 아스키코드
      return num
  
  num = atoi("1234")
  print(type(num), num)
  ```

  

### 패턴 매칭

- 패턴 매칭에 사용되는 알고리즘
  - **고지식한 패턴 검색 알고리즘** 개념부터 구현까지 알기!
  - 카프-라빈 알고리즘
  - KMP 알고리즘
  - 보이어-무어 알고리즘

- 고지식한 패턴검색 알고리즘
  
- `i = i - j` 같아진 갯수만큼 빼버린다.
  
- KMP 알고리즘

  - 전처리: pattern을 보고 접두어와 접미어가 같은 것 찾기 -> 되돌아갈 자리 찾기

- 보이어-무어 알고리즘

  - rithm 문자열의 skip 배열에서 m은 0이 아니라 5칸 띄기

  #### 연습문제 3

- 고지식한 방법을 이용하여 패턴을 찾아 봅시다

- 임의의 본문 문자열과 찾을 패턴 문자열을 만들기

- 결과 값으로 찾은 위치 값을 결과로 출력

  ```python
  # 라이브
  ```

  ```python
  # 나
  def BruteForce(p, t):
      j = 0 # p의 index
      i = 0 # t의 index
      M = len(p)
      N = len(t)
      while j < M and i < N:
          if t[i] != p[j]:
              i = i - j
              j = - 1
              # j = 0 했더니 if를 만족하지 않을때 j값이 증가하지 않는다.
          i = i + 1 # t와 p가같거나,틀린경우(if처리후) 주어진 문자열에서는 다음 idx
          j = j + 1 # t와 p가 같을 경우 j는 다음idx, 다를 경우 처음으로[0]
      if j == M: 
          return i - M
      else: 
          return -1
  
  print(BruteForce('abc', 'abc'))
  ```

  ```python
  # 온라인 코칭
  def 고지식패턴(str1, str2):
      A = len(str1)
      B = len(str2)
      
      for i in range(A-B+1):
          cnt = 0
          for j in range(B):
              if str1[i+j] == str2[j]:
                  cnt += 1
          else:
              break
      if cnt == B:
          print("여기서부터 일치", i)
          return i
     return -1
  ```

  

### 그 외

- is와 ==

  - ==은 값 비교, is는 객체 비교( 튜터에서 화살표 가르키는거)

    ```python
    a = [1, 2, 3]
    b = a
    c = [1, 2, 3]
    ```



# 오늘의 요약

- 키워드
  - 유니코드
  - 문자열 처리
  - 문자열 뒤집기/ 비교/ 교체하기- (atoi, itoa)
  - 패턴 매칭 - 고지식한 패턴 검색(BruteForce)

- 유니코드

  - 컴퓨터에서 영문자를 표현하기 위해서는 7bit짜리 ASCII 코드를 사용하고, 다국어를 표현하기 위해서는 유니코드를 사용한다.
  - 유니코드는 저장하는 변수의 크기를 정하지 않고, 바이트 순서에 대해서 표준화하지 못했기 때문에 파일 인식 시 변수의 크기와 바이트 순서를 인식하고 구분하는 외부 인코딩이 필요하다.

- 문자열 처리

  - python은 ''와 ""를 구분하지 않는다.
  - 인덱스로 접근 가능, 슬라이싱 연산 가능하지만 요소값을 변경할 수 없다(immutable)
  - 요소값을 변경하려면 list로 변환 후 변경하고 다시 string으로 변환해줘야 한다.

- 문자열 뒤집기/ 비교/ 교체

  - 뒤집기: 자기 문자열

    - swap을 이용한다. python은 임시 변수가 필요없다.
    - `str_rev`
      - List로 변환 후 swap, 다시 List

  - 비교: 

  - 교체

    - `atoi`, `itoa`

      - 강의 다시보기

      - (데이터 / 10) + 머시기

      - **'0'의 아스키코드를 기준**

      - ```python
        num *= 10 으로 자릿수 맞추기
        ```

- 패턴 매칭

  - 고지식한 패턴 검색

    - 주어진 문자열 t와 찾을 패턴 p의 인덱스 i, j 가 동시에 움직인다.

    - `i = i - j` 같아진 갯수만큼 빼버린다.

      



