# Interrupt

> 2020.10.21



## 1. Interrupt

> HW에 의해 이벤트가 발생했을 때 interrupt가 발생하며, HW 이벤트를 알려주는 메커니즘이다.



### 1.1 Communication with hardware

- Polling : 하드웨어에 이벤트가 발생했는지 주기적으로 체크하는 방법으로, CPU의 낭비가 심하다.
- Interrupt : 이벤트가 발생하면 CPU로 signal을 보내며, 현재 진행 중인 작업을 중단하고 `Interrupt service routine`을 따라 interrupt를 handling 한다.



### 1.2 Interrupt handling

- 인터럽트는 프로세스들보다 더 높은 우선순위를 갖는다.
  - 인터럽트가 발생하면, 현재 실행 중인 프로세스는 CPU를 반환하고 ISR이 실행된다.
- **Interrupt handling stpes**
  1. 현재 실행 중이던 프로세스의 context를 저장한다. (PC)
  2. 인터럽트 번호를 사용하여 해당 ISR 주소를 찾는다.
  3. ISR 주소로 PC를 update한다.
  4. ISR을 실행하고 이전에 실행하던 프로세스를 실행한다.



### 1.3 Advice related to ISR

- ISR은 block 상태로 될 수 없다. 인터럽트가 block 상태가 되면, system dead lock에 걸린다.
- ISR의 실행시간은 짧아야 한다. 이전에 실행되고 있던 프로세스가 멈춘 상태이므로, 빠르게 재동작시키기 위함이다.

- **ack(확인응답) : 송신된 메세지가 정상적으로 수신되었음을 송신측으로 확인응답하는 것**

  

