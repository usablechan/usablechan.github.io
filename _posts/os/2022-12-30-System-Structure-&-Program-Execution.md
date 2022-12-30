---
title: "System Structure & Program Execution"
excerpt:

categories:
  - os
tag:
  - 스터디
  - 강의

toc: true
toc_sticky: true
toc_label: "contents"

last_modified_at: 2022-12-30
---

![Untitled](/assets/images/os/2-1.png)

### 전체적인 흐름

CPU가 controller한테 input 요청함 → 기다리는동안 다른 프로그램에게 CPU제어권 넘겨서 다른거 실행중 → I/O controller가 CPU한테 intrrupt를 걸음 → CPU 제어권이 다시 운영체제한테 넘어감→ 입력받은 값을 아까 입력 요청한 프로그램 메모리 공간에 copy함 → 실행하던 프로그램 마저 실행하게 cpu제어권 줌

### CPU

- 클럭마다 메모리에서 명령을 하나씩 읽어와서 실행함
- I/O 가 일어나면 직접 접근하지 않고 Device Controller 에게 시킴
  → 왜 why? cpu에 비해서 디바이스 속도가 너무 느려서
- 메인 메모리와 local buffer에 접근 가능

### memeory

- cpu가 직접 접근 할 수 있는 내부 기억 장치
- 특정 프로그램이 cpu에서 실행되려면 해당부분이 메모리에 올라가 있어야함

### mode bit

: CPU의 제어권이 `운영체제` 에 있는지 `사용자 프로그램`에 있는지 알려줌

사용자 프로그램의 나쁜짓으로 다른 프로그램 및 운영체제에 피해가지 않게 하기 위해서

- 1 `사용자 모드` - 사용자 프로그램
  - 메모리, I/O device 등의 대한 접근 제한됨
- 0 `커널 모드` - 운영체제

### 타이머

- 정해진 시간 동안 제어권을 갖도록 설정
  → CPU를 특정 프로그램이 독점하는 것을 막기 위해
- 타이머 값이 0이 되면 타이머 interrupt 발생

### device controller

- I/O 장치를 관리하는 일종의 작은 CPU
- 제어정보를 위한 control register, status register 가짐
- 작업공간인 local buffer 가짐
- `device driver` : device를 제어하는 역활을 하는 프로그램 → software
- `device controller` : 일종의 작은 CPU → hardware

### DMA(direct memory access)

- memery에 대한 접근을 cpu만 할 수 있음
  → 매 interrupt마다 cpu는 하던 일 멈추고 memory 접근해서 I/O 데이터를 쓰니까 비효율적
  ⇒ 메모리에 접근 할 수 있는 DMA을 둠

1. I/O 발생하면 DMA가 memory에 기록함
2. I/O 가 어느정도 쌓여서 일정 크기(block)을 넘어가면 dma가 cpu한테 이런 일 있었다고 일러바침(interrupt)

- memory controller는 dma와 cpu 동시에 메모리 접근하는 것을 방지함

### 입출력의 수행

- 모든 입출력 명령은 `특권명령`
- 사용자 프로그램 어떻게 I/O 함?
  - 시스템콜 : 사용자프로그램이 운영체제 커널을 호출하는 걸 말함
    일반적인 함수 호출이랑 다름 ( 사용자모드 권한 문제) → 사용자 프로그램이 interrupt 발생시킴 → 운영체제야 해줘!
  - I/O 올바른요청인지 확인
  - OS가 I/O controller에게 요청
  - 제어권이 다른 프로그램 넘어갔다가 I/O 받으면 interrupt(hardware) 발생

### interrupt

> CPU가 프로그램을 실행하고 있을 때, 입출력이나 예외상황 등의 처리가 필요한 경우 CPU에게 알리는 이벤트

- interrupt (하드웨어 인터럽트): 하드웨어가 발생시킨 인터럽트
- trap (소프트웨어 인터럽트)
  - exception : 프로그램 오류
  - system call : 프로그램이 커널 함수 호출
- 관련용어
  - `인터럽트 벡터` : 인터럽트 종류 마다 어디있는 함수를 실행해야하는지 정의해놓은 거
  - `인터럽트 처리 루틴` : 인터럽트 별로 어떤 일을 해야하는 지 적혀있는 함수

---

### pc register

![Untitled](/assets/images/os/2-2.png)

- cpu가 pc(programcounter register)에서 instruction 주소를 가져와서 실행함.
- pc + 4 해서 다음 명령어 가르킴
- 다음 instruction을 실행하기 전에 interrupt 들어왔는지 확인
- 지금 헷갈리는 것
  64bit 시스템에서는 pc 값이 8씩 증가했었나?
  risc 시스템 말고 cisc 시스템에서는 +4 증가시키는 건가 아닌가 헷갈림

---

### 동기식 입출력과 비동기식 입출력

![Untitled](/assets/images/os/2-3.png)

- 돟기식 입출력
  - I/O 요청 후에 입출력 기다린 다음에 하던 일 이어함
  - read 해서 data를 사용해야할 때 주로 사용?
  - 방법1. 그냥 I/O 기다림
    - CPU 리소스 낭비
    - 매순간 하나의 I/O만 사용하는 거니까 I/O 리소스도 낭비
  - 방법2. 기다리는 동안 다른 프로그램 실행
    - 기다리는 동안 다른 프로그램 실행
- 비동기식 입출력
  - I/O 요청 후에 입출력 기다리지 않고 입출력과 무관한 일을 처
  - read 해오는 data와 관련없는 일을 처리하거나, write 일 때 주로 사용
- 두 가지 모두 interrupt를 통해서 I/O의 완료를 알림

### 서로 다른 입출력 명령어

![Untitled](/assets/images/os/2-4.png)

일반 적인 I/O 방식과, memory mapped I/O 방식이 있음

- memory mapped : I/O device에도 메모리 주소에 연장 주소 붙여서 주소로 접근가능

### 저장장치 계층 구조

![Untitled](/assets/images/os/2-5.png)

- primary storage
  - cpu 에서 직접 접근 가능한 저장장치 ( executable 라고 함 )
  - 휘발성
- secondary storage
  - 섹터 단위로 읽기 때문에 cpu가 직접 접근 못함
  - 비휘발성
- 속도와 가격, 용량에서의 trade off 관계를 가짐
- `caching` : 하위 계층에서 필요한 정보들을 상위계층에 저장해서 재사용하는 방법을 말함

### 프로그램의 실행

![Untitled](/assets/images/os/2-6.png)

- `physical memory` : memory 계층을 말하며, os가 실행되면 커널이 가장 먼저 physical memory 최하단에 할당
- `virtual memory` : 프로세서 마다 할당 받는 가상적인 공간
  - 각 프로그램 마다 0번으로 시작하는 주소공간을 할당받음
  - virtual address는 physical address로 변환되는 과정을 거침
  - 프로세스의 일부분은 memory에 일부분은 swap area에 위치한다.
- `swap area` 는 storage를 메모리의 연장공간 처럼 사용하는 곳
  - 휘발성을 가
- `file system` 은 storage에 실행파일들을 담아두는 곳
- code : cpu 에서 실행할 기계어 코드 저장
- data : 전역 변수 등 프로그램이 사용하는 데이터 저장
  - main함수 전에 선언되어 프로그램의 시작과 동시에 할당되고 프로그램이 종료되어야 메모리에서 소멸됨
- stack :
  - 함수로 호출될 때, 함수의 수행을 마치고 복귀할 주소 및 데이터를 임시 저장
  - 지역 변수들도 저장

### 커널 주소 공간의 내용

![Untitled](/assets/images/os/2-7.png)

- code
  - os 관련된 코드들
- data
  - 각종 자원을 관리하기 위한 자료구조들이 저장
  - cpu나 메모리 같은 하드웨어 자원, 프로세스 관리하기 위한 자료구조들
  - PCB : 각 프로그램을 관리하기 위한 자료구조
- stack
  - 프로그램 스택 영역과 마찬가지로 함수 호출시의 복귀 주소 및 데이터 저장
  - 현재 수행중인 프로세스 마다 별도의 스택을 두어 관리
      <aside>
      💡 시스템 콜이나, 인터럼트 등으로 os↔️프로그램 과정에서 각 프로그램으로 복귀할 주소 및 데이터를 저장하기 위해
      
      </aside>

### 사용자 프로그램이 사용하는 함수

- 사용자 정의 함수
  - 직접 정의한 함수
- 라이브러리 함수
  - 직접 정의하지 않고 갖다 쓴 함수
- 커널 함수
  - 운영체제의 프로그램 함수

![Untitled](/assets/images/os/2-8.png)

- 커널 함수로의 호출은 커널 주소 공간으로의 jump가 해야하는데 이게 불가능함
  → 시스템콜을 통해서 커널 함수를 실행함

### 프로그램 실행

![Untitled](/assets/images/os/2-9.png)

---

### 퀴즈

<details> <summary>Q. CPU를 특정 프로그램이 독점하는 것을 막기 위한 하드웨어 장치</summary>
<div markdown="1">

&nbsp;&nbsp;&nbsp; A.타이머

</div>
</details>

<details> <summary>Q. 프로그램에서 사용자로부터 입력을 받아올 때, softwafe interrupt만 발생한다(O/X)</summary>
<div markdown="1">

&nbsp;&nbsp;&nbsp; A. X 프로그램이 시스템콜(softwafe intterupt)를 발생시키고, I/O 장치가 입력을 받은 뒤에 cpu에 hardware interrupt를 발생시킴

</div>
</details>

<details> <summary>Q. 사용자 프로그램은 사용자의 입출력을 위해서 I/O device에 직접 접근할 수 있다.(O/X)</summary>
<div markdown="1">

&nbsp;&nbsp;&nbsp; A. X 사용자 모드에서는 접근이 제한되어 시스템 콜을 통한 우회

</div>
</details>
---

### reference

- [http://www.kocw.net/home/search/kemView.do?kemId=1046323](http://www.kocw.net/home/search/kemView.do?kemId=1046323)
- [https://steady-coding.tistory.com/511](https://steady-coding.tistory.com/511)
- [https://steady-coding.tistory.com/513](https://steady-coding.tistory.com/513)
