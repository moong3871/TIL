# TIL_algo

- DFS

  ```python
  # 수도 코드만 보고 짜보기
  # visited[v] <- True: 방문 체크해
  # v와 이어진 w 중에서
  # 방문 안한곳은 재귀호출(DFS)
  # 다 돌았으면 return
  def DFS(v):
      visited[v] = 1
      for w in range(?): # Node가 1부터 N까지니까 ? = N+1
          if G[v][w] == 1 and visited[w] != 1: 
              return DFS(w)
      return ?
  ```

- 사다리 문제

  ```python
  # 도착지점에서 출발점 찾기
  def DFS(y, x):
      visit.append((y, x)) #방문 표시
      if y == 0: # 출발점 찾으면 그때의 x 출력
          print(x)
      dy = (0, 0, -1) # 아래로만
      dx = (-1, 1, 0) # 좌,우
      for i in range(3):# 델타탐색으로 양옆,위 탐색?
          Y = y + dy[i]
          X = x + dx[i]
          if 0 <= Y < 100 and 0 <= X < 100 and arr[Y][X] == 1 and (Y, X) not in visit:
              return DFS(Y, X)
  for _ in range(10):
      tc = int(input())
      arr = [list(map(int, input().split())) for _ in range(100)]
      visit = []
      print('#{}'.format(tc), end=" ")
      DFS(99, arr[99].index(2)) # 도착지점을 찾아야 하므로
      						# 마지막 열에서 2의 inx값 빼내기
  ```

  ```python
  #100x100크기의 2차원배열을 받는다
  # '0'으로 채워져있고 연속된 사다리는 '1', 도착지점은 '2'로 표현됨
  # 출발점 x=0~x=9가 있는데 세로 방향의 두 막대 사이에 임의의 막대들이 랜덤 간격으로 추가됨
  #아래 방향으로 진행하면서 좌우 방향으로 이동 가능한 통로가 나타나면 방향을 전환함
  #방향 전환 후 다시 아래 방향으로만 이동, 바닥에 도착하면 멈춤
   
  #dfs로 풀어야되는문제.........
  #1.2차원배열을 입력받는다
  #2.첫줄에서 1인 값 찾기 -> list에 담아두기,아닐때 그다음값으로 바로 넘어감
  #3.양 옆중 1이 나올때까지 밑으로 내려감 -> 복잡한거 함수로 만들면 편함
  #옆에 1이 나왔다면 방향전환
  #방향전환 후 다시 옆에 1이 나올때까지 내려감
  #만약 2가 없다면 다시 첫줄에 방문하지 않은 1로 들어감
  #반복...............................?
   
  #위에 계속 써먹을 것들을 올리고
  #그밑에 함수를 만들어야 함수에서도 적용이 됨!
   
   
  #방향..델타...
  di = [0,0,1,-1] #오른쪽, 왼쪽, 아래, 위 #여기서 위는 필요없음
  dj = [1,-1,0,0]
  ladder = [] #함수에서 사용될 ladder선언
  #ni는 다음 위치, ni=i+di[방향] 그러면 옮겨짐!, nj도 마찬가지
   
  def check(i,j,dir): #x,y,방향 인자로 받음
      #종료조건!!!!(중요)
      if ladder[i][j] == 2:
          return True #종료이면 True...본문에서 조건식으로 시작지점 나오게함
   
      #종료조건 1개더인데 끝일때!!! 2가아니면 False를 반환
      elif i == 99:
          return False
   
      else:
          #방향을 설정해줄거야
          #초반 방향은 무조건 아래부터 시작!!
          #오른쪽, 왼쪽으로 갈때 그 방향을 우선시해줌! 아래로 내려갈땐 옆을 봐줌...ㅠㅠ
          #dir은 방향의 idx임, idx가 0이면 오른쪽, 1이면 왼쪽, 2면 아래
          #di[dir]
          if (dir == 0) or (dir == 1): #오른쪽이나 왼쪽을 볼때 해당 방향을 우선시해줄거야
              #다음 위치를 변수로 만들건데 현위치(i)에 방향을 더함..ㅎ
              ni, nj = i + di[dir], j + dj[dir]
              #그 다음 위치가 out of idx가 됐는지 아닌지 체크해줘야됨, 그리고 옆이 1일때!!!!
              if ni >= 0 and ni < 100 and nj >= 0 and nj < 100 and ladder[ni][nj] == 1:
                  return check(ni,nj,dir)
              else: #못갔어, 그러면 아래로(dir=2) 내려감!!!!
                  return check(i+1,j,2)
   
          else:#애초에 아래로 내려가는 중...dir=2
              #양옆을 우선 확인!!! 배열밖인지 ,1인지 확인한뒤, 1이면 방향전환 아니면 내려감!!!!
              #오른쪽(0) 왼쪽(1)이기 때문에 for문을 돌릴거야!
              for d in range(2): #d가 dir
                  ni,nj = i + di[d], j + dj[d]
                  if ni >= 0 and ni < 100 and nj >= 0 and nj < 100 and ladder[ni][nj] == 1:
                      return check(ni,nj,d)
                  #만약 if가 false면 그냥 다음으로 넘어감!
              #for문이 끝났는데, return이 안됐다는건 idx가 밖이거나 양옆이 1이 아니라는것! 그럼 내려가....!
              return check(i+1,j,2) #아래로 내려가!!!!!!!
           
   
          #
          # #보기편하게 변수로 설정해줌
          # #왼쪽
          # li = i
          # lj = j-1
          # #idx가 나가지않게 먼저 체크해주는게 중요함!
          # if (li >= 0) and (li < 100) and (lj >= 0) and (lj < 100):
          #     #옆이 1이면 방향전환
          #     if ladder[li][lj] == 1:
          #         #재귀로 만든다..
          #         #다음 위치의 좌표도 옆에 1이 있는지 확인,check(li,lj,dir)
   
   
   
   
  for tc in range(1,11):
      T = int(input())
      #1 이차원배열 받기
      ladder = [list(map(int,input().split())) for _ in range(100)]
      #2 출발점들을 start 리스트에 넣기! 열이기 떄문에 j...
      start = []
      for j in range(100):
          if ladder[0][j] == 1:
              start.append(j)
      #3 출발점을 하나씩 빼올거야! s가 j임
      for s in start:
          #기본방향은 밑으로 내려갈거고, 출발점은 행이 0이고, 열이 s임
          #check의 return 값이 True니까...if로...해줌....답을 찾았으니 그 출발점인 s를 출력하게 해라!
          if check(0,s,2):
              print('#{} {}'.format(tc,s))
              break #답을 찾았기 떄문에 나가줌!!!!
  ```

  ```python
  def dfs(a,b):
      global result
      visited.append((a,b))
      #맨위에 가면 멈추기
      if a == 0:
          result = b
          return
      #델타 탐색으로 위 양옆 탐색 후 이동
      for d in range(3):
          new_x = a + d_x[d]
          new_y =b + d_y[d]
          if (0<= new_x < 100) and (0<= new_y < 100) and (arr[new_x][new_y]==1) and ((new_x,new_y) not in visited):
              return dfs(new_x,new_y)
   
  for _ in range(10):
      tc = int(input())
      arr = [list(map(int,input().split())) for _ in range(100)]
      visited = []
      d_x = [0, 0, -1]
      d_y = [-1, 1, 0]
      result = 0
      dfs(99,arr[99].index(2))
   
      print('#{} {}'.format(tc, result))
  ```

  ```python
  def find_route(a,b) : # 델타탐색 안쓰고 직접 idx 바꾸기
      visited.append((a,b))
      if a == 0 :
          return b
      if 0<=b+1<100 :
          if mat[a][b+1] and (a, b+1) not in visited :
              return find_route(a, b+1)
      if 0<= b-1 <100 :
          if mat[a][b-1] and (a, b-1) not in visited :
              return find_route(a, b-1)
      return find_route(a-1, b)
          
  for t in range(10) :
      N = int(input())
      mat = []
      for i in range(100) :
          row = list(map(int, input().split()))
          mat.append(row)
      a, b = 99, mat[99].index(2)
      #result = 0
      visited=[]
      result = find_route(a,b)
      print('#{} {}' .format(N, result))
  ```

  

