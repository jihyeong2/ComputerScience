[TOC]

# Race Condition

> 2020.10.25



## 1.  Race Condition

> 멀티 프로세싱 시스템에서 동일한 공유 자원에 둘 이상의 프로세스나 쓰레드에서 접근하여, 의도치 않은 경우를 초래하는 것을 의미한다.





### 1.1 Race Condition이 발생하는 경우

1. 커널 작업을 수행하는 도중에 인터럽트 발생

   - 문제점 : 커널 모드에서 데이터를 로드하여 작업을 수행하다가 인터럽트가 발생하여 같은 데이터를 조작하는 경우
   - 해결법 : 커널모드에서 작업을 수행하는 동안, 인터럽트를 disable시켜 CPU 제어권을 가져가지 못하도록 한다.

2. 프로세스가 `System Call`하여 커널 모드로 진입하여 작업을 수행하는 도중 `Context Switching` 발생

   - 문제점 : 프로세스 1이 커널모드에서 데이터를 조작하는 도중, 시간이 초과되어 CPU 제어권이 프로세스 2로 넘어가 같은 데이터를 조작하는 경우
   - 해결법 : 프로세스가 커널모드에서 작업을 하는 경우 시간이 초과되어도 CPU 제어권이 다른 프로세스에게 넘어가지 않도록 함.

3. 멀티 프로세서 환경에서 공유 메모리 내의 커널 데이터에 접근할 때

   - 문제점 : 멀티 프로세서 환경에서 2개의 CPU가 동시에 커널 내부의 공유 데이터에 접근하여 조작하는 경우
   - 해결법 : 커널 내부에 있는 각 공유 데이터에 접근할 때마다, 그 데이터에 대한 lock/unlock을 하는 방법

   

### 1.2 SpinLock

- 어느 프로세스가 요청한 자원이 다른 프로세스에 의해 점유되어 있는 상태이면, block 상태가 되어 Context Switching이 발생하게 되어 CPU Idle Time이 증가하게 된다. 이를 방지하고자 Spinlock을 사용한다.
- Spinlock은 lock을 불러오지 못할 경우, block 상태로 바꾸지 않고, lock을 얻을 때까지 무한정 대기하는 `busy waitiing`



**[참고]**

- https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/OS#%EB%8F%99%EA%B8%B0%EC%99%80-%EB%B9%84%EB%8F%99%EA%B8%B0%EC%9D%98-%EC%B0%A8%EC%9D%B4
- https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Operating%20System/Race%20Condition.md

