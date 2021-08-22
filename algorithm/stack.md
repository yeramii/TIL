## Stack

자료를 쌓아올리는 방식으로 저장하는 방법

<br>

#### 특징

* 특정 데이터 타입이 없기 때문에, `list`를 스택처럼 사용한다.
* 자료를 선형으로 저장할 저장소
  * 자료 간의 관계가 1:1이다.
  * 마지막 삽입된 원소의 위치를 `top` 이라고 한다.
* LIFO

<br>

#### 구현

* 연산
  * 삽입 : `push`
  * 삭제 : `pop`
  * 공백인지 아닌지 확인 : `isEmpty` => `len`
  * `top`에 있는 item 반환 : `peek` => `[-1]`
* `top` (= stack pointer) 을 이용해야 동작이 빠르다. 

```python
# push : top을 하나 올리고 그 위치에 삽입
def push(n):
	top += 1
	stack[top] = n

# pop : top 위치 원소를 빼고 top 하나 내림
# 지우는 동작은 따로 하지 않아도 된다. (어차피 push가 새로 덮어쓰니까)
def pop():
	# 보통 여기서 len = 0 검사하지 않고, pop을 쓰기 전에 있는지 검사한다.
	top -= 1
	return stack[top + 1]
```

* 사용 데이터
  * 1차원 배열
    * 구현이 용이하지만, 스택의 크기를 변경할 수 없다.
  * 동적 연결리스트
    * 구현이 복잡하지만, 메모리를 효율적으로 사용한다.
    * 메모리 상에서 연결된 대신에, 분리된 메모리 덩어리들을 만들고, 다음 메모리의 주소를 함께 저장한다.

<br>

#### 응용

* 괄호 검사
  * 왼쪽 괄호와 오른쪽 괄호의 개수가 같아야 한다.
  * 왼쪽 괄호는 오른쪽 괄호보다 먼저 나와야 한다.
  * 괄호 사이에는 포함 관계만 존재한다.
* function call
  * 프로그램에서의 함수 호출과 복귀에 따른 수행 순서를 관리
  * 가장 마지막에 호출된 함수가 가장 먼저 실행을 완료하고 복귀하는 후입선출 구조이므로, 후입선출 구조의 스택을 이용
  * 과정
    * 함수 호출이 발생하면 함수 수행에 필요한 지역변수, 매개변수 및 수행 후 복귀할 주소 등의 정보를 stack frame에 저장하여 system stack에 삽입
    * 함수 실행이 끝나면 system stack의 top원소 (stack frame)를 삭제(pop)하면서 프레임에 저장되어 있던 복귀 주소를 확인하고 복귀
    * 위 과정의 반복으로 전체 프로그램 수행이 종료되면 system stack은 공백 스택이 된다.

<br>

#### 재귀 호출

* 자기 자신을 호출하여 순환 수행되는 것

* 컴퓨터가 내부적으로 재귀 호출할 때 스택을 이용

* 멈출 값(경계)을 인자로 받아, 점점 증가하는 값으로 호출할 수 있다.

* 피보나치 수를 구하는 함수

  * 엄청난 중복호출이 존재
  * 시간 복잡도 : O(n^2) = 오메가(n^2)

  ```python
  def fibo(n):
      global cnt
      cnt += 1
      if n < 2:
          return n
      else:
          return fibo(n-1) + fibo(n-2)
  
  cnt = 0
  print(fibo(20), cnt)
  ```

<br>

#### Memoization

* 이전에 계산한 값을 메모리에 저장해서 매번 다시 계산하지 않도록 하여, 전체적인 실행 속도를 빠르게 하는 기술

* 동적 계획법의 핵심이 되는 기술

* 피보나치 수를 구하는 함수

  * 시간복잡도 : O(n)

  ```python
  n = 20
  
  # 1. stack의 크기가 정해져 있지 않은 경우
  def fibo1(n):
      if n >= 2 and len(memo1) <= n:
          memo1.append(fibo1(n-1) + fibo1(n-2))
      return memo1[n]
  
  memo1 = [0, 1]
  print(fibo1(n))
  
  
  # 2. stack의 크기가 미리 정해져 있는 경우 - better
  def fibo2(n):
      global cnt
      cnt += 1
      if n >= 2 and memo2[n] == 0:
          memo2[n] = fibo2(n-1) + fibo2(n-2)
      return memo2[n]
  
  memo2 = [0] * (n + 1)
  memo2[0] = 0
  memo2[1] = 1
  cnt = 0
  print(fibo2(n), cnt)
  ```

<br>

#### DP (Dynamic Programming)

* 동적 계획 알고리즘은 그리디 알고리즘과 같이 최적화 문제를 해결하는 알고리즘이다.

* 구현

  1. 입력 크기가 작은 부분 문제들을 모두 해결
  2. 그 해들을 이용하여 보다 큰 크기의 부분 문제들을 해결
  3. 최종적으로 원해 주어진 입력의 문제를 해결

* 피보나치 수를 구하는 함수

  * memoization과 달리, 재귀 없이 테이블에서 값을 가져온다.
  * memoization을 재귀적 구조에 사용하는 것 (recursive)보다, 반복적 구조로 DP를 구현한 것 (iterative)이 성능 면에서 보다 효율적이다.

  ```python
  def fibo(n):
      table[0] = 0
      table[1] = 1
      for i in range(2, n + 1):
          table[i] = table[i-1] + table[i-2]
      return table[n]
  
  n = 20
  table = [0] * (n + 1)
  print(fibo(n))
  ```

<br>

#### DFS (Depth First Search, 깊이우선탐색)

* 시작 정점의 한 방향으로 깊이 탐색해 가다가 더 이상 갈 곳이 없게 되면, 가장 마지막에 만났던 갈림길 간선이 있는 정점으로 되돌아와서 다른 방향의 정점으로 탐색을 계속 반복하여 결국 모든 정점을 방문하는 순회 방법

* 가장 마지막에 만났던 갈림길의 정점으로 되돌아가서, 다시 깊이우선탐색을 반복해야 하므로 LIFO 구조의 stack 활용

* 구현

  1. 시작 정점 v를 결정하여 방문

  2. 정점 v에 인접한 (연결된) 정점 중에서

     a. 방문하지 않은 정점 w가 있으면, 정점 v를 스택에 push하고 정점 w를 방문한다. 그리고 w를 v로하며 다시 2. 를 반복

     b. 방문하지 않은 정점이 없으면, 탐색의 방향을 바꾸기 위해서 스택을 pop하여 받은 가장 마지막 방문 정점을 v로 하여 다시 2. 를 반복

  3. 스택이 공백이 될 때까지 2. 를 반복

  ```python
  # V => 노드, 정점
  # E => 엣지, 간선
  V, E = list(map(int, input().split()))
  
  # E 쌍의 개수 들어옴 -> 2 * E 개
  graph_list = list(map(int, input().split()))
  
  graph = [[0 for _ in range(V + 1)] for _ in range(V + 1)]
  visited = [0 for _ in range(V + 1)]
  
  for i in range(E):
      start = graph_list[2*i]
      end = graph_list[2*i + 1]
  
      graph[start][end] = 1
      graph[end][start] = 1
  
  def dfs(v):
      global graph, visited, V
  
      # stack에 시작점을 넣고 시작
      stack = [v]
  
      # stack이 비어있지 않다면 계속해서 DFS 진행
      while len(stack):
          # 가장 최근에 넣었던 위치를 빼온다
          v = stack.pop()
  
          # 마지막 위치가 방문하지 않은 곳이라면
          if visited[v] == 0:
              # 방문한다
              visited[v] = 1
              print('방문한 위치 {0} visited {1}'.format(v, visited))
  
              # 시작점을 기준으로 한 줄 반복 (0번 노드는 없으니 1부터 시작)
              for w in range(1, V + 1):
                  # 간선이 있고, 방문하지 않았다면
                  if graph[v][w] == 1 and visited[w] == 0:
                      # 스택에 추가
                      stack.append(w)
  
  # dfs를 1번 노드를 기준으로 탐색
  dfs(1)
  ```

  










