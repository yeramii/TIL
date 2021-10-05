# Queue

큐의 뒤에서는 삽입만 하고, 큐의 앞에서는 삭제만 이루어지는 구조

<br>

#### 특징

* stack과 마찬가지로 삽입과 삭제의 위치가 제한적인 자료구조
* FIFO
  * 머리인 `front`와 꼬리인 `rear`로 이뤄진다.
  * `front` : 마지막 삭제 위치 (or 저장된 원소 중 첫 번째 원소)
  * `rear` : 마지막 저장 위치

<br>

### 선형큐

#### 연산

* `enQueue(item)` : 큐의 뒤쪽 (`rear` 다음)에 원소를 삽입
* `deQueue()` : 큐의 앞쪽 (`front`)에서 원소를 삭제하고 반환
* `createQueue()` : 공백 상태의 큐를 생성
* `isEmpty()` : 큐가 공백상태인지 확인
* `isFull()` : 큐가 포화상태인지 확인
* `Qpeek()` : 큐의 앞쪽 (`front`)에서 원소를 삭제없이 반환

#### 구현

```python
# 1. 공백 큐 생성
def createQueue():
	Q = [0] * 100
	front = -1
	rear = -1
		
# 2. 원소 A 삽입
def enQueue(A):
	global rear
	if isFull():
		print("Queue Full")
	else:
		rear += 1
		Q[rear] = 'A'

# 3. 원소 반환/삭제
# 실제로 삭제되진 않았지만, deQueue한 원소는 다시 접근할 일이 없기 때문에 삭제된 거나 마찬가지!
def deQueue():
	if isempty():
		# 비어있음을 출력하는 함수
		Queue_Empty()
	else:
		front += 1
		return Q[front]

# 4. 공백 및 포화상태 검사
def isEmpty():
	return front == rear

def Full():
	return rear == len(Q) - 1

# 5. 가장 앞에 있는 원소 검색/반환
def Qpeek():
	if isEmpty():
		print("Queue Empty")
	else:
		return Q[front + 1]
```

#### 장점

* test case 별 큐를 생성하지 않고, `front`, `rear` 만 초기화해서 값을 덮어쓰면 되서 유용
* 일정량을 모아서 사용하는 경우에 유용

#### 문제점 : 잘못된 포화상태 인식

* 삽입과 삭제를 계속할 경우, 배열의 앞 부분에 활용할 수 있는 공간이 있어도, `rear = n-1` 인 상태(포화상태)로 인식하여 더 이상의 삽입 X

#### 해결방법

* 매 연산이 이루어질 때마다 저장된 원소들을 한 칸씩 앞으로 이동시킴 -> 원소 이동에 많은 시간 소요 -> 효율성 급감
* 1차원 배열을 사용하되, 논리적으로는 처음과 끝이 연결되어 원형 형태의 큐를 이룬다고 가정

#### [Python 실습] 함수 만들지 않고 데이터 삽입/삭제

1. 특정 크기의 빈 리스트 - 가장 빠름

   ```python
   Q = [0] * 10    # 10칸 짜리 큐
   front = -1
   rear = -1
   
   rear += 1
   Q[rear] = 1     # enQueue(1)
   rear += 1
   Q[rear] = 2     # enQueue(2)
   rear += 1
   Q[rear] = 3     # enQueue(3)
   
   while front != rear:
       front += 1
       print(Q[front], end=' ')    # deQueue()
       print(Q, front, rear)
   
   '''
   [출력]
   1 [1, 2, 3, 0, 0, 0, 0, 0, 0, 0] 0 2
   2 [1, 2, 3, 0, 0, 0, 0, 0, 0, 0] 1 2
   3 [1, 2, 3, 0, 0, 0, 0, 0, 0, 0] 2 2
   '''
   ```

2. deque - 중간 빠름

   ```python
   from collections import deque
   
   # enqueue -> append
   q = deque()
   q.append(1)
   q.append(2)
   q.append(3)
   
   # dequeue -> popleft
   while q:
       print(q.popleft(), end=' ')
       print(q)
   
   '''
   [출력]
   1 deque([2, 3])
   2 deque([3])
   3 deque([])
   '''
   ```

3. 빈 리스트 - 가장 느림

   ```python
   listQ = []
   listQ.append(1)
   listQ.append(2)
   listQ.append(3)
   
   while listQ:
       print(listQ.pop(0), end=' ')
       print(listQ)
   
   '''
   [출력]
   1 [2, 3]
   2 [3]
   3 []
   '''
   ```

<br>

### 원형큐

* 초기 공백 상태 : `front = rear = 0`
* index의 순환 : 나머지 연산자 `mod`를 사용
* `front` : 공백 상태와 포화 상태 구분을 쉽게 하기 위해 `front`가 있는 자리는 사용하지 않고 빈자리로 둠
  * 포화 상태 : `front = (rear + 1) % len(queue)`

#### 구현

```python
# 1. 공백 큐 생성
def createQueue():
	cQ = [0] * 100
	front = 0
	rear = 0

# 2. 공백 및 포화 상태 검사
def isEmpty():
	return front == rear
def isFull():
	# 삽입할 rear의 다음 위치 = 현재 front
	return (rear + 1) % len(cQ) == front

# 3. 삽입
def enQueue(item):
	global rear
	if isFull():
		print("Queue Full") # 디버깅용
		# 꽉 찼을 때 할 수 있는 선택
		# 1. 나중에 들어온 애들 위에 덮어씀
		# 2. 오래 있었던 애들 위에 덮어씀
		# 파이참의 콘솔버퍼는 cyclic queue라서 콘솔 입력이 1MB 이상이면 앞부터 덮어씀
	else:
		rear = (rear + 1) % len(cQ)
		cQ[rear] = item

# 4. 삭제
# 4-1. front 값을 조정하여 삭제할 자리를 준비
def deQueue():
	global front
	if isEmpty():
		print("Queue Empty")
	else:
		front = (front + 1) % len(cQ)
		return cQ[front]
# 4-2. 새로운 front 원소를 리턴하여 삭제와 동일한 기능 (return만 없음)
def delete():
	global front
	if isEmpty():
		print("Queue Empty")
	else:
		front = (front + 1) % len(cQ)
```

<br>

### 연결큐

* 저장할 데이터가 너무 커서 한 번에 넣을 공간이 없을 때, 연결 리스트를 사용
* 큰 덩어리를 나눠서 다른 위치의 메모리에 저장하고, 데이터와 함께 다음 덩어리의 위치를 저장

#### 단순 연결 리스트(Linked List)를 이용한 큐

* 큐의 원소 : 단순 연결 리스트의 노드
* 큐의 원소 순서 : 노드의 연결 순서. 링크로 연결되어 있음
* `front` : 첫 번째 노드를 가리키는 링크
* `rear` : 마지막 노드를 가리키는 링크

#### 구현

```python
class Node:
    def __init__(self, item, n=None):
        self.item = item
        self.next = n

# 1. 원소 삽입
def enQueue(item):
    global front, rear
    newNode = Node(item)    # 새로운 노드 생성
    if front == None:       # 큐가 비어있다면
        front = newNode
    else:
        rear.next = newNode
    rear = newNode

# 2. 공백 상태 검사
def isEmpty():
    return front == None

# 3. 원소 반환/삭제
def deQueue():
    global front, rear
    if isEmpty():
        print("Queue Empty")
        return None

    item = front.item
    front = front.next
    if front == None:
        rear = None
    return item

# 4. 첫 번째 원소 삭제 없이 반환
def Qpeek():
    return front.item

# 5. 모든 원소를 공백으로 구분된 문자열로 반환
def printQ():
    f = front
    s = ''
    while f:
        s += f.item + ' '
        f = f.next
    return s
```

<br>

### 우선순위 큐

* 우선순위를 가진 항목들을 저장하는 큐
* FIFO가 아니라, 우선순위가 높은 순서대로 먼저 나간다.

#### 배열/리스트를 이용한 우선순위 큐

* 가장 앞에 최고 우선순위의 원소가 위치
* 배열을 사용하므로, 삽입이나 삭제연산에서 원소의 재배치가 발생
  * 이에 소요되는 시간이나 메모리 낭비가 크다.

#### 적용 분야

* simulation system
* network traffic control
* OS의 task scheduling

<br>

### Buffer

* 데이터를 한 곳에서 다른 한 곳으로 전송하는 동안 일시적으로  그 데이터를 보관하는 데이터 영역
* buffering : 버퍼를 활용하는 방식 혹은 버퍼를 채우는 동작
* FIFO 방식인 큐를 활용하여 구현할 수 있다.

<br>

### BFS (Breath First Search)

* 탐색 시작점의 인접한 정점들을 먼저 모두 차례로 방문한 후에, 방문했던 정점을 시작점으로 하여 다시 인접한 정점들을 차례로 방문하는 방식
  * 시작점으로부터 간선의 개수가 같은 순서 (중복을 피하기 위해 체크할 배열을 따로 만든다.)
* 인접한 정점들에 대해 탐색한 후 차례로 다시 BFS를 진행해야 하므로, FIFO 구조의 queue 활용

#### 구현

```python
# G: 그래프, v: 시작점, N: 정점 개수
def BFS(G, v):
    # 큐 생성후, 시작점 enqueue
	visited = [0] * (N + 1)
	queue = []
	queue.append(start)
    # 큐가 비어있지 않다면
	while queue:
        # 첫 번째 원소 dequeue
		v = queue.pop(0)
        # 방문되지 않은 경우, 표시하고 할 일 함
		if not visited[v]:
            visited[v] = True
			visit(v)
            # v에 연결된 모든 정점에 대해, 방문되지 않은 것 enqueue하고 방문(거리) 표시
			for w in G[v]:
				if not visited[w]:
                    queue.append(w)
                    visited[w] = visited[v] + 1
```







