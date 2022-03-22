# How to get input

### 1. input()

- 한두 줄 입력받을 때 사용한다.

- 반복문으로 여러 줄을 입력받을 때는 `input()`으로 입력받으면 시간초과가 발생할 수 있다.

<br>

### 2. sys.stdin.readline()

- 임의의 개수의 정수를 입력받아 리스트에 저장할 때

  ```python
  import sys
  data = list(map(int, sys.stdin.readline().split()))
  ```

  - 문자열 형태로 저장되므로, 형변환을 거쳐야 한다.
  - `split()`은 공백을 기준으로 문자열을 나눈다.

- 문자열 n줄을 입력받아 리스트에 저장할 때

  ```python
  import sys
  n = int(sys.stdin.readline())
  data = [sys.stdin.readline().strip() for _ in range(n)]
  ```

  - `sys.stdin.readline()`은 한 줄 단위로 입력받기 때문에, 개행문자가 같이 입력되므로 제거해야 한다.
  - `strip()`은 문자열 양 끝의 공백문자를 제거한다.
