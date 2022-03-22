# How to get infinite input

### 1. sys.stdin.readlines()

```python
import sys

lines = sys.stdin.readlines()
for line in lines:
    A, B = map(int, line.split())
    print(A + B)
```

- `sys.stdin.readlines()` 구문을 사용하여 파일의 끝 부분까지 한 번에 가져온다.

- 가져온 내용 안에서 한 줄씩 읽는다.

- 각 줄이 문자열이 되어 문자열의 리스트로 저장된다.

  ex) `lines = ['1 1\n', '2 2\n', '3 3']`

<br>

### 2. EOFError

```python
while True:
    try:
        A, B = map(int, input().split())
        print(A + B)
    except EOFError:
        break
```

- 계속 진행되는 반복문을 만들고, 그 안에서 예외 처리한다.

> 입력 도중에 파일의 끝을 만나면 EOFError가 발생한다. (EOF: 파일의 끝(End of File))