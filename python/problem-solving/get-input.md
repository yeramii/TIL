# How to get input

### 1. input()

- input()이 호출되면 인자로 주어진 문자를 화면에 출력하고 사용자의 입력을 기다린다.
- 사용자가 키를 누르면 그에 대응하는 데이터가 하나씩 버퍼에 들어간다.
- 개행 문자는 입력의 종료로 간주한다.
- 무엇을 입력하든 문자열로 변환하고 줄 바꿈을 제거한 뒤 값을 반환한다.

- 활용
  - 한두 줄 입력받을 때 사용한다.
  - 반복문으로 여러 줄을 입력받을 때는 `input()`으로 입력받으면 시간초과가 발생할 수 있다.

<br>

### 2. sys.stdin.readline()

- input()과 달리 문자를 화면에 출력하지 않는다.
- 한 번에 읽을 수 있는 글자 수 크기를 매개변수로 제공한다.
- 한 번에 읽어와 버퍼에 저장하기 때문에, 하나씩 누를 때마다 데이터픞 버퍼에 저장하는 input()보다 빠르며 입력이 많아질수록 차이가 커진다.
- 활용
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

<br>

### 3. conclusion
- input() 은 문자열 변환, 줄 바꿈 제거 등 추가적인 과정이 있고, 데이터가 하나씩 버퍼에 들어간다.
- sys.stdin.readline() 은 문자열 변환, 줄바꿈 제거 등 과정이 없으며, 데이터가 한번에 버퍼에 들어가므로 input() 보다 빠르다.
- code 제출
  - input()을 사용하는 경우, import sys 가 필요 없다.
  - sys.stdin.readline()을 사용하는 경우, import sys 도 코드에 포함하여 제출한다. 
