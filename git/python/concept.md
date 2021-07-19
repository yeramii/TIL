
### Module

* 일반적으로는 큰 system을 이해하기 쉽게 기능별로 나눈 작은 단위를 뜻한다.
* Python 에서는 ".py" Python 파일 1개를 뜻한다.



### Package

* Python 의 용어, 모듈의 모음을 뜻한다.
* 주로 인터넷에서 Package 단위로 가져와 쓴다.

#####   from [A] import [B]

* 특정 Package에서 특정 모듈만 불러오는 것이 가능
* 특정 모듈의 특정 함수, 변수만 불러오는 것이 가능

#####   import 모듈

*  특정 모듈 전체를 import
* C언어에서 include 역할



### Library

* 소스코드를 가져다 쓸 수 있도록, 함수/클래스들로 구현된 소스코드 모음을 나타내는 개념
* Package도 Library라고 할 수 있다.
* 모듈 하나만 있어도, Library라고 할 수 있다.

#### => Module < Package < Library



### Framework

* 처음부터 개발하는 것이 아니라, 소스코드 뼈대 위에서 작성하는 것을 뜻한다.
* 뼈대를 다운로드 받아 개발을 시작하면 생산성이 올라간다.
* 초보자들도 내부가 튼튼한 결과물을 얻을 수 있다.
* 대신, Framework를 사용하면 만들어지는 결과물이 비슷한 느낌을 받는다.

* python 웹 프레임워크 순위 : Flask, Django





# How to use Python

1. Python shell : 단순 test 용도
2. Python IDLE : Python의 대표 IDE
3. OS shell에서 Python Script 실행
4. PyCharm 사용



### Shell

##### OS는 "커널 + shell + app" 으로 구성
  * Kernel : OS의 핵심 소스코드
  * Shell : 사용자가 OS에 명령을 내릴 수 있는 UI 프로그램

##### OS에서 Shell

  * GUI (Graphic User Interface) : 그래픽 환경으로 시스템 제어 

    ex. 윈도우 바탕화면

  * CLI (Command User Interface) : 명령어를 통해 시스템 제어 

    ex. 윈도우 DOS모드(Disk OS), 리눅스 SSH 모드(Secure Shell)

##### Python Shell

  : Python 내부에 명령어를 던져 결과를 볼 수 있는 UI

#####  Window Shell 3가지

  * Window Shell : 일반적으로 사용하는 GUI
  * cmd : DOS 시절부터 사용되던 Shell
  * Power Shell : 리눅스의 sh 대항마

##### Linux에서 Shell

* GNOME : 리눅스 그래픽 Shell (GUI)
* csh : 리눅스 CLI





# Python Script

### Script

코드 일정 단위로, 번역(컴파일) 없이 실행 가능한 내용을 뜻함

##### Script를 Run 시키는 프로그램

* Script는 번역이 없어, 해당 명령어를 CPU가 이해할 수 없다.
* 묶음 단위의 Script를 즉시 실행해주는 프로그램(= Runtime) 이 필요하다.
* Runtime이 지속적으로 CPU가 이해할 수 있도록 번역해줘야 하기 때문에 속도가 느리다.



### Script Language vs Complie Language

##### Compile Language

* "Build 후 Run" 을 해야 실행 결과를 확인 가능 (Build : 컴파일 + 링킹)
* C / C++은 CPU가 이해할 수 있는 CPU Instruction으로 변환이 필수
* 따라서 Runtime이 없이 즉시 CPU가 빠르게 수행

##### Script Language

* Python은 "Run"을 하면 실행 결과 확인 가능



### Runtime

* 실행기 (Runtime Env.), 실행시간 (Runtime) 이라는 두 가지 의미가 있다.
* Runtime Error는 실행기 에러가 아니라, 실행시간 중 나오는 에러를 뜻한다.
* 근래 컴파일 언어도 App의 플랫폼 독립성을 위해 Runtime을 둔다.

##### Runtime Env.

* 실행기 역할을 위한 도구 모음

* Interpreter 포함 (Compiler도 포함할 수 있음)
* Common Library
* Utility (Garbage Collector)

##### Interpreter

* 소스 코드를 즉시 번역하여 실행하는 프로그램



### 언어와 Runtime

##### Python Runtime

* CPython : Python 기본 Runtime 환경
* IronPython : MS에서 만든 Runtime 환경
* PyPy : CPython보다 더 빠른 Runtime

##### JavaScript

* Runtime : Node.js
* Java와 연관성이 없는 언어

##### Java

* Runtime 이름 : JRE (Java Runtime)



### Runtime 장점 = 플랫폼 독립

Script 파일만 있으면 어떤 Device에서도 동작 (미리 장비에 Runtime 설치) 

