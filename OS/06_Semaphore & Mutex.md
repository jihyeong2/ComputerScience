[TOC]

# Semaphore & Mutex

>  2020.10.25



## 1. Syncronization

> 동기화는 메소드를 실행시킴과 동시에 반환 값이 기대되는 경우를 동기화라고 표현하고, 그렇지 않은 경우 비동기라고 표현한다. `동시에` 라는 의미는 값이 반환되기 전까지는`block` 상태에 있다는 의미이다. 비동기의 경우는 `block`상태로 바뀌지 않고 이벤트 큐에 넣거나, 백그라운드 스레드에게 해당 작업을 위임하고 바로 다음 코드를 실행하기 때문에 기대되는 값이 바로 반환되지 않는다.



### 1.1 Critical Section 

> 멀티 프로세스 환경에서 둘 이상의 프로세스가 동시에 접근해서는 안되는 공유 자원의 코드 영역이다. 

- 해결법 : 하드웨어 기반 해결책으로, 동시에 공유 자원에 접근하는 것을 막기 위해 Critical Section에 진입하는 프로세스는 Lock을 획득하고 Critical Section을 빠져나올 때, Lock을 방출함으로써 동시에 자원에 접근할 수 없도록 한다.



### 1.2 Critical Section 해결책

> 3가지 조건을 충족하면 해결할 수 있다.



1. 상호배제 : 하나의 프로세스가 임계구역에 들어가 있으면 다른 프로세스는 들어갈 수 없다.
2. 진행 : Critical Section에 들어가 있는 프로세스가 없다면, 어느 프로세스가 들어갈 것인지 적절하게 선택해야 한다.
3. 한정 대기 : `Infinite Starvation`을 방지하기 위해, 한 번 들어갔다 나온 프로세스는 다음에 들어갈 때 제한을 준다.



## 2. Mutex & Semaphore

> 공유 자원에 대한 접근권한, Lock이라는 키를 한 개만 갖고 있는 것은 뮤텍스이고, 여러 개 가질 수 있는 것은 세마포어이다.



### 2.1 Mutex

- `이진 세마포어`라고도 불리우며, Lock을 갖고 있을 때에만 공유 데이터에 접근이 가능하다.
- Lock을 갖고 있는 프로세스나 쓰레드만이 Lock을 해제할 수 있다.



### 2.2 Semaphore

- 세마포어는 동시에 리소스에 접근할 수 있는 `task의 개수`를 의미한다.

- Semaphore는 정수 값을 갖는 변수이며, P와 V라는 명령어에 의해서만 접근할 수 있다.
- P는 Critical Section에 들어가기 전에 수행되고, V는 Critical Section에서 나올 때 수행된다. 이 때 Semaphore 변수를 수정하는 연산은 모두 '원자성'을 만족해야 한다. 즉, 한 프로세스나 한 쓰레드에서 값을 변경하는 동안에는 다른 프로세스나 쓰레드가 **동시에 접근해서 변경할 수 없다.**
- 값이 0보다 크면 접근을 허용하되 1을 감소하고, 값이 0이면 접근을 막고 해당 프로세스를 block시킨다. 반대로 작업이 끝난 프로세스나 쓰레드가 나갈 때는 값을 1 증가시켜 block 상태인 프로세스를 ready 상태로 바꾸고 자원에 접근할 수 있도록 한다.



**[참고]**

- https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Operating%20System/Operation%20System.md

- https://slenderankle.tistory.com/197