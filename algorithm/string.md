## String

* python에서, 시퀀스 자료형으로 분류되고, 시퀀스 자료형에서 사용할 수 있는 인덱싱, 슬라이싱 연산을 사용할 수 있다.
* java에서, 문자열 데이터를 저장, 처리해주는 String 클래스를 제공한다.
* c언어에서, 문자열은 문자들의 배열 형태로 구현된 응용자료형이므로, 문자배열에 문자열을 저장할 때는 항상 마지막에 끝을 표시하는 널문자('\0')를 넣어줘야 한다.

<br>

### Pattern matching

* 데이터를 검색할 때 특정 패턴이 출현하는지, 또한 어디에 출현하는지 등을 특정하는 방법

* 사용 알고리즘
  * 고지식한 패턴 검색 알고리즘 (Brute Force)
  * 카프-라빈 알고리즘
  * KMP 알고리즘
  * 보이어-무어 알고리즘

<br>

#### Brute Force algorithm

* 본문 문자열을 처음부터 끝까지 차례대로 순회하면서 패턴 내의 문자들을 일일히 비교
* 시간복잡도 : O(mn)

```python
# 1. 고지식한 패턴 검색 - 첫 패턴
def BruteForce_1(p, t):
    """
    패턴을 찾을 때까지 모든 인덱스를 순회한다.

    :param p: 찾을 패턴
    :param t: 전체 텍스트
    :return: 패턴을 찾으면 해당 인덱스(constant), 못 찾으면 -1.
    """
    M = len(p)
    N = len(t)
    for i in range(N - M + 1):
        for j in range(M):
            if t[i + j] != p[j]:
                break
        if j == M - 1:
            return i
    return -1


# 2. 고지식한 패턴 검색 - 모든 패턴
def BruteForce_2(p, t):
    """
    모든 인덱스를 순회하며 패턴을 있는대로 찾는다.
    
    :param p: 찾을 패턴
    :param t: 전체 텍스트
    :return: 패턴을 찾으면 모든 패턴의 시작 인덱스(list), 못 찾으면 -1.
    """
    M = len(p)
    N = len(t)
    lst = []
    i = 0

    while i <= N - M:
        for j in range(M):
            if t[i + j] != p[j]:
                break
        if j == M - 1:
            lst.append(i)
            i += M
        else:
            i += 1

    if lst == []:
        return -1
    else:
        return lst
```

<br>

#### Rabin-Karp algorithm

* 시간복잡도 : O(m + n)

<br>

#### KMP algorithm

* 불일치가 발생한  앞 부분을 이미 알고 있으므로, 앞 부분에 대해선 다시 비교하지 않음
* 패턴을 전처리하여 배열 next[M]을 구해서 잘못된 시작을 최소화
* 시간복잡도 : O(m + n)

##### 사전 지식

* Degenerate pattern : 어떤 패턴 속에 있는 작은 패턴이 한 번 이상 반복되는 현상

* LPS (Longest proper prefix which is suffix) : Prefix와 Suffix가 같은 경우 중 가장 길이가 긴 경우의 길이

```python
  ### Prefix, Suffix 찾기
  ABX
  # Prefix : A, AB
  # Suffix : X, BX
  
  
  ### LPS 구하기
  pat = 'ABXAB'
  # Prefix : A, AB, ABX, ABXA
  # Suffix : B, AB, XAB, BXAB
  # lps : AB
  
  lps[0] = 0	# prefix와 suffix가 없으므로, 0
  lps[1] = 0	# prefix와 suffix가 일치하지 않으므로, 0
  lps[2] = 0	# prefix와 suffix가 일치하지 않으므로, 0
  lps[3] = 1	# A가 일치하므로 1
  lps[4] = 2	# AB가 일치하므로 2
  
  lps = [0, 0, 0, 1, 2]
```

##### 코드

```python
def computeLPS(p, lps):
    """
    주어진 문자열의 lps 배열을 만든다.

    :param p: 주어진 문자열
    :param lps: lps 배열을 저장할 리스트
    :return: 없음
    """
    # length of the previous longest prefix suffix
    leng = 0

    # 항상 lps[0]==0 이므로 while 문은 i==1 부터 시작
    i = 1
    while i < len(p):
        # 이전 인덱스에서 같았다면 다음 인덱스만 비교
        if p[i] == p[leng]:
            leng += 1
            lps[i] = leng
            i += 1
        else:
            # 일치하지 않는 경우
            if leng != 0:
                # 이전 인덱스에서는 같았으므로 leng 을 줄여서 다시 검사
                leng = lps[leng - 1]
                # 다시 검사해야 하므로 i는 증가하지 않는다.
            else:
                # 이전 인덱스에서도 같지 않았다면 lps[i]는 0이고, i는 1 증가
                lps[i] = 0
                i += 1

def KMPSearch(p, t):
    """
    텍스트에서 패턴을 찾으면 해당 인덱스를 출력한다.

    :param p: 찾을 패턴
    :param t: 전체 텍스트
    :return: 없음
    """
    M = len(p)
    N = len(t)
    lps = [0] * M

    # Preprocess the pattern
    computeLPS(p, lps)

    i = 0   # index for t
    j = 0   # index for p
    while i < N:
        # 문자열이 같은 경우 양쪽 인덱스를 모두 증가
        if p[j] == t[i]:
            i += 1
            j += 1
        # Pattern 찾지 못한 경우
        elif p[j] != t[i]:
            # j!=0 인 경우는 짧은 lps에 대해 재검사
            if j != 0:
                j = lps[j - 1]
            # j==0 이면 일치하는 부분이 없으므로 인덱스 증가
            else:
                i += 1

        # Pattern 찾은 경우
        if j == M:
            print("Found pattern at index " + str(i - j))
            # 이전 인덱스의 lps 값을 참조하여 계속 검색
            j = lps[j - 1]
```

<br>

#### Boyer-Moore algorithm

* 오른쪽에서 왼쪽으로 비교
* 텍스트 문자를 다 보지 않아도 된다.
* 대부분의 상용 소프트웨어에서 채택하고 있는 알고리즘
* 시간복잡도 : 최악은 O(mn), 최선은 O(n) 이하.

```python
```



