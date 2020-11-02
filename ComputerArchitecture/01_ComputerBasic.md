# Computer Basic

> 2020.10.29



## 1. Computer Architecture Basic

> 컴퓨터 시스템은 크게 하드웨어와 소프트웨어로 나뉜다.
>
> 하드웨어 : 컴퓨터를 구성하는 기계적 장치
>
> 소프트웨어 : 하드웨어의 동작을 지시하고 제어하는 명령어 집합



### 1.1  Hardware

> 중앙처리장치(CPU)
>
> 기억장치 : RAM, HDD
>
> 입출력장치 : 마우스, 키보드
>
> 하드웨어는 CPU, 기억장치, 입출력장치로 구성되어 있으며, 이들은 시스템 버스로 연결되어 있다. 시스템 버스는 데이터와 명령 제어 신호를 각 장치로 실어나르는 역할을 한다.

- 중앙처리장치 (CPU)
  - 주기억장치에서 프로그램 명령어와 데이터를 읽어와 처리하고 명령어의 수행 순서를 제어한다. 
  - CPU는 비교와 연산을 담당하는 **산술논리연산장치(ALU)**와 명령어의 해석과 실행을 담당하는 **제어장치**, 속도가 빠른 데이터 기억장소인 **레지스터**로 구성되어있다.
- 기억장치
  - 프로그램, 데이터, 연산의 중간 결과를 저장하는 장치이다. 
  - 주기억장치와 보조기억장치로 나뉘며, RAM과 ROM 모두 이곳에 해당한다. 실행중인 프로그램과 같은 프로그램에 필요한 데이터를 일시적으로 저장한다. 
  - 보조기억 장치는 하드디스크 등을 말하며, 주기억장치에 비해 속도는 느리지만 많은 자료를 영구적으로 보관할 수 있는 장점이 있다.
- 입출력장치
  - 입력 장치는 컴퓨터 내부로 자료를 입력하는 장치로 키보드, 마우스 등이 있다.
  - 출력 장치는 컴퓨터에서 외부로 자료를 출력(표현)하는 장치로 모니터, 스피커 등이 있다.
- 시스템 버스
  - 하드웨어 구성 요소를 물리적으로 연결하는 선으로, 각 구성요소가 다른 구성요소로 데이터를 보낼 수 있도록 통로 역할을 한다.
  - 용도에 따라 데이터 버스, 주소 버스, 제어 버스로 나뉜다.
- 데이터 버스
  - 중앙처리장치와 기타 장치 사이에서 데이터를 전달하는 통로이다.
  - 기억장치와 입출력장치의 명령어와 데이터를 중앙처리장치로 보내거나, 중앙처리장치의 연산 결과를 기억장치와 입출력장치로 보내는 **양방향** 버스이다.

- 주소 버스
  - 데이터를 전송하기 위해서는 기억장치의 **주소**를 설정해주어야 한다.
  - 주소 버스는 CPU가 주기억장치나 입출력장치로 주소를 전달하는 통로이기 때문에 **단방향** 버스이다.
- 제어 버스
  - 주소 버스와 데이터 버스는 모든 장치에 공유되기 때문에 이를 제어할 수단이 필요하다. 제어 버스는 CPU가 기억장치나 입출력장치에 제어 신호(기억장치 읽기/쓰기, 버스 요청 및 승인, 인터럽트 요청 및 승인, 클락, 리셋 등)를 전달하는 통로이다.
  - 제어버스는 읽기 동작과 쓰기 동작을 모두 수행하기 때문에 **양방향** 버스이다.
  - 컴퓨터는 기본적으로 읽고 처리한 뒤 저장하는 과정으로 이루어지며, 이 과정을 통해 끊임없이 주기억장치(RAM)과 소통한다. 만약 운영체제가 64-bit라면, CPU는 RAM으로부터 데이터를 한 번에 64-bit 읽어온다.



## 2. High-level language to machine code



### 2.1 HW/SW Stack in Computer

- Applicatios : Application SW로, High-level language로 쓰여진다.
- System software 
  - Compilers : High-level language를 Machine code로 번역한다.
  - Operating systems : Input/Output을 다루며, memory management, task scheduling & sharing resources의 일을 한다.
- BIOS : Basic Input/Output System
- Instruction Set Architecture(ISA)  : HW와 Low-level language 사이의 interface
- Computer Hardware : Processor, Memory, I/O controllers



### 2.2 Instruction

- 쉽게 말해 명령어라고 칭하며, 컴퓨터 언어의 말들이다.
- Instruction(명령어)의 집합체를 **Instruction Set**이라 한다.
- CPU마다 Instruction set이 다르다.



### 2.3 High-level Code to Assembly to Executable

![image-20201029112803075](./img/highLevelCodeToAssembly.png)

[출처] : 서울과학기술대학교 전자IT미디어공학과 컴퓨터구조 수업자료

- compiler와 assembler에 의해 binary data 번역된 Instructions와 data가 메모리에 저장되며, CPU는 이를 실행하기 위해 fetch한다.



### 2.4 CrossCompiler

- 위에서 언급했듯이, CPU마다 사용하는 Instruction set이 다르다고 했다. 그러면 MIPS를 사용하기 위해서는  MIPS machice이 필수적으로 있어야 하나??
- 이러한 문제를 해결해주는 것이 **CrossCompiler**이다.
- **CrossCompiler**는 compile 하려는 플랫폼을 다른  compiler로 compile하는 것이다.



**[참고]**

- https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Computer%20Architecture/%EC%BB%B4%ED%93%A8%ED%84%B0%EC%9D%98%20%EA%B5%AC%EC%84%B1.md