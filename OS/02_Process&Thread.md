---
typora-copy-images-to: img
---

[TOC]

# 프로그램과 프로세스

> 2020.10.21



## 1. 프로그램과 프로세스의 개념

> 프로그램 : 프로그램은 하드 디스크에 저장되어 있는 것(ex. 한글, 워드)
>
> 프로세스 : 프로그램이 실행 상태로 실제 구현된 것.

**프로그램이 실행되면 HW Resource에 CPU와 Memory가 할당된다. 프로그램은 하드디스크에 한 개만 저장되지만, 프로세스는 여러 개가 생길 수 있다. (ex. 여러 개의 인터넷 창)**



### 1.1 Process State

![process_state](C:\Users\qmffn\Desktop\ComputerScience\OS\img\process_state.jpg)

- running : CPU를 할당받고 실행 중인 상태
- ready : CPU를 할당받고 있지 않지만, 즉시 run 할 수 있도록 대기하고 있는 상태
- block : 어떠한 이벤트를 기다리거나, 자연스럽게 CPU에서 할당되어진 것이 release 되어진 상태
  - 기다리고 있는 이벤트가 발생하기 전까지는 실행할 수 없다.
  - 이벤트가 발생하면 바로 ready state로 바뀐다.
  - block state는 CPU allocation의 candidate가 아니다. block state는 이벤트가 있기 까지 실행 할 수 없으므로 CPU에 아무런 변화가 생기지 않는다. 즉, useless / resource 낭비이기 때문이다.

**하드디스크에 저장되어 있는 프로그램이 execution되면 process가 생성되고, memory에 process를 저장하는 공간이 생성된다.**



### 1.2 Process Address Space

> 메모리에 있는 프로세스를 담는 공간으로, memory에 4개의 별도공간이 생긴다.



- Code segment : Program의 실행 Code가 저장된다. (Read-only) -> 공유
- Data segment : 전역변수(Process life time과 같다고 할 수 있다.)와 같은 프로그램의 Data가 저장된다. (Read-Write)

- Stack segment : Function을 호출하는 정보와Function 안의 지역변수(함수가 종료되면 지역변수는 Memory에서 제거된다.)들을 저장한다. (Read-Write)

- Heap : Dynamic memory allocation (malloc함수 사용 시 heap 영역이 사용됨.)



- Code segment가 분리되어 있는 이유
  - Program code는 같은 프로그램이라면 모두 동일한 code를 갖고 있다. 즉, 하나의 프로그램은 여러 프로세스를 가질 수 있는데 실행을 위한 code는 동일하다는 의미이다.
  - 그렇기 때문에 여러 개의 프로세스가 프로그램 코드를 공유하기 위해 분리하였고, 메모리 사용량 또한 줄였다.
  - Data, Stack은 각각의 process에서 사용되는 변수들은 같은 프로그램임에도 불구하고 달리 쓰일 수 있기 때문에 공유하지 않는다.



- Stack이 Data와 분리되어 있는 이유
  - Stack은 함수 호출과 지역변수를 저장하는데, 이를 위해서는 LIFO 구조인 stack이 적합하기 때문에 분리시켰다.



### 1.3  Multi Programming

- CPU를 공유하면서 두 개 이상의 프로세스가 실행되는 컴퓨팅 환경이다.
- **Process Management : CPU Resource Allocation을 위해 OS는 live process를 계속 추적해야 하고, 각각의 process state를 추적해야한다.**
  - 효율적이고 공정한 CPU Scheduling
  - Protection between processes
  - Syncronization between processes
  - Memory allocation



### 1.4 Process Metadata & PCB

- Process Metadata는 각 Process ID, Process state, Process priority와 같이 프로세스가 갖고 있는 중요한 정보들을 말한다.
  - Process ID는 다른 프로세스와 구별을 위해 unique 해야 한다.
  - priority는 각 프로세스들마다 중요도가 다르기 때문에 OS는 프로세스의 우선순위를 항상 추적해야한다.
- PCB(Process Control Block)
  - 구조체로 되어 있으며, 프로세스의 메타데이터가 PCB에 저장되어 있다.
  - 각각의 PCB는 하나의 PCB를 갖는다. (Unique)
  - 프로세스의 중요한 것들이 모두 PCB에 저장되어 있으므로, OS는 PCB만을 추적하면 된다.
  - PCB는 메모리에 따로 저장된다. (Process Address Space 외의 다른 공간)



- **How to keep track of live process?**
  - live process끼리 서로 연결시켜 linked list로 관리해줌으로써 이를 해결
  - 프로세스가 생성되면(프로그램이 실행되면) PCB가 생성되고, 생성된 PCB는 live PCB의 헤드 혹은 먼저 연결되어 있던 live PCB와 연결된다.
  - 각각의 PCB들은 기본적으로 before와 next 두 개의 PCB와 연결되어 있다.
  - **그렇기 때문에 OS는 여러 개의 linked list가 존재한다. **
    - **linked list for live processes**
    - **linked list for ready processes**(레디 상태인 프로세스는 Candidate of CPU Scheduling이므로 ready list를 따로 갖는다.)



