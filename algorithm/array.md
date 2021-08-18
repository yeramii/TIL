## Array

일정한 자료형의 변수들을 하나의 이름으로 열거하여 사용하는 자료구조

<br>

#### Array Iterations

* n x m 배열의 n * m 개의 모든 원소를 빠짐없이 조사하는 방법

* 행 우선 순회, 열 우선 순회, 지그재그 순회

  ```python
  # 1. 행 우선 순회
  for r in range(len(array)):
      for c in range(len(array[r])):
          print(r, c)
  
  # 2. 열 우선 순회
  for c in range(len(array[0])):
      for r in range(len(array)):
          print(r, c)
  
  # 3. 지그재그 순회
  for r in range(len(array)):
      for c in range(len(array[0])):
          print(r, c + (r % 2) * (len(array[0]) - 2 * c))
  ```

* 델타 이용한 탐색

  ```python
  # 4. 델타 이용한 탐색
  result = array[:]
  dr = [0, 1, 0, -1]
  dc = [1, 0, -1, 0]
  k = 0
  cnt = 1
  r, c = 0, -1
  
  while cnt <= len(array) * len(array[0]):
      nr, nc = r + dr[k], c + dc[k]
      if 0 <= nr < len(array) and 0 <= nc < len(array[0]) and result[nr][nc] == 0:
          print(nr, nc)
          result[nr][nc] = cnt
          cnt += 1
          r, c = nr, nc
      else:
          k = (k + 1) % 4
          
  print(result)
  ```

<br>

#### Subset

* 집합의 원소가 n개일 때, 공집합을 포함한 부분집합의 수는 2n개

```python
# 1. 각 원소가 부분집합에 포함되었는지 확인하고 부분집합을 생성
bit = [0, 0, 0, 0]
for i in range(2):
    bit[0] = i
    for j in range(2):
        bit[1] = j
        for k in range(2):
            bit[2] = k
            for l in range(2):
                bit[3] = l
                print(bit)

# 2. 비트 연산자 활용
arr = [1, 2, 3, 4]
n = len(arr)
subset = []

# 0000 ~ 1111
for i in range(1 << n):
    temp = []
    # 0 ~ 3
    for j in range(n):
        # i의 j번째가 1이면 해당 위치 원소 추가  
        if i & (1 << j):
            temp.append(arr[j])
    subset.append(temp)
print(subset)
```

<br>

#### Search

* 저장되어 있는 자료 중에서 원하는 항목을 찾는 작업

* 순차 검색(sequential search)

  * 일렬로 되어 있는 자료를 순서대로 검색하는 방법
  * 시간복잡도 : O(n)

  ```python
  # 1. 순차 검색 (sequential search) - 정렬된 경우
  def sequentialSearch_1(lst, key):
      """
      리스트의 첫 인덱스부터 마지막 인덱스까지 순회하며 찾는 항목과 일치하는 지 검사한다.
      
      :param lst: 주어진 리스트
      :param key: 찾을 항목
      :return: 찾은 경우, 항목의 인덱스(idx). 못 찾은 경우, -1.
      """
      idx = 0
      n = len(lst)
      while idx < n and lst[idx] != key:
          idx += 1
      if idx < n:
          return idx
      else:
          return -1
  
  # 2. 순차 검색 (sequential search) - 정렬되어 있지 않은 경우
  def sequentialSearch_2(lst, key):
      """
      리스트의 첫 인덱스부터 순회하며, 찾는 항목보다 크거나 같은 항목이 나오면 멈춘다.
      
      :param lst: 주어진 리스트
      :param key: 찾을 항목
      :return: 찾은 경우, 항목의 인덱스(idx). 못 찾은 경우, -1.
      """
      idx = 0
      n = len(lst)
      while idx < n and lst[idx] < key:
          idx += 1
      if idx < n and lst[idx] == key:
          return idx
      else:
          return -1
  ```

* 이진 검색(binary search)

  * 자료의 가운데에 있는 항목의 키 값과 비교하여 다음 검색의 위치를 결정하고 검색을 계속 진행하는 방법
  * 자료가 항상 정렬된 상태를 유지해야 한다.
  * 시간복잡도 : O(log n)

  ```python
  # 3. 이진 검색 (binary search)
  def binarySearch_1(lst, key):
      """
      검색 범위를 반으로 줄여가며 보다 빠르게 검색을 수행한다.
      
      :param lst: 주어진 리스트
      :param key: 찾을 항목
      :return: 찾은 경우, 항목의 인덱스(idx). 못 찾은 경우, -1.
      """
      start = 0
      end = len(lst) - 1
      while start <= end:
          middle = (start + end) // 2
          if lst[middle] == key:
              return middle
          elif lst[middle] > key:
              end = middle
          else:
              start = middle
      return -1
  
  # 4. 이진 검색 (binary search) - 재귀 함수 이용
  def binarySearch_2(lst, low, high, key):
      """
      검색 범위를 반으로 줄여가며 보다 빠르게 검색을 수행한다.
      
      :param lst: 주어진 리스트
      :param low: 찾을 범위의 하한
      :param high: 찾을 범위의 상한
      :param key: 찾을 항목
      :return: 찾은 경우, 항목의 인덱스(idx). 못 찾은 경우, -1.
      """
      if low > high:
          return -1
      else:
          middle = (low + high) // 2
          if key == lst[middle]:
              return middle
          elif key < lst[middle]:
              return binarySearch_2(lst, low, middle, key)
          elif lst[middle] < key:
              return binarySearch_2(lst, middle, high, key)
  ```

* 해쉬(hash)

<br>

#### Exhaustive Search

* 문제의 해법으로 생각할 수 있는 모든 경우의 수를 나열해보고 확인하는 기법

#### Greedy Algorithm

* 최적 해를 구하는데 사용되는 근시안적인 방법
* 그 순간에 최적이라고 생각되는 것을 선택해 나가는 방식

#### Selection Algorithm

* 저장되어 있는 자료로부터 k번째로 큰/작은 원소를 찾는 방법
* 자료를 정렬한 후, 원하는 순서에 있는 원소를 가져오는 과정으로 이뤄진다.

<br>





