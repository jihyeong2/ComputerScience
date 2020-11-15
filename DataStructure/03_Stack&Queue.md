# Stack & Queue

> 2020.11.15



#### Stack

- **Last In First Out (LIFO)**방식의 자료구조로, 입력과 출력이 한 곳으로 제한되어 있다.

- **Stack**은 함수의 콜스택을 구현할 때 자주 사용되며, 문자열 관련 알고리즘 문제와 DFS를 구현할 때 사용된다.
- Stack에서 필요한 메서드는 **데이터를 추가하는 push(), 데이터를 삭제하는 pop()**이다. Stack은 가장 마지막에 push된 데이터를 가리키는 **StackPointer(SP)**가 있고, push()하면 해당 SP에 데이터를 삽입하고, SP를 1 증가시킨다. pop()을 하면 해당 SP의 데이터를 초기화하고, SP를 1 감소시킨다.



**구현**

```python
class Stack():
    def __init__(self):
        self.s=[]

    def push(self,data):
        self.s.append(data)
    def pop(self):
        if len(self.s)==0:
            return -1
        return self.s.pop(-1)
    def top(self):
        if len(self.s)==0:
            return -1
        return self.s[-1]
```



#### Queue

- **First In First Out(FIFO)**방식의 자료구조로, 입력과 출력이 양쪽 끝(front,rear)으로 제한되어 있다.
- **Queue**는 버퍼를 구현할 때 자주 사용되며, BFS 알고리즘을 풀 때에도 사용된다.
- Queue에서 필요한 메서드는 **데이터를 추가하는 enqueue(), 데이터를 삭제하는 dequeue()**이다. 큐의 가장 첫번째 데이터를 가리키는 **front**가 있고, 마지막 데이터를 가리키는 **rear**가 있다.  enqueue()를 하면 현재 rear가 추가할 데이터를 가리키고, rear를 1 증가시키고, dequeue()를 하면 front가 가리키는 데이터를 빼고, front를 1 증가시킨다.



**구현**

```python
class queue():
    def __init__(self):
        self.q=[]
        self.front=-1
        self.rear=-1

    def enqueue(self,data):
        self.q.append(data)
        self.rear+=1

    def dequeue(self):
        if self.front==self.rear:
            return -1
        self.front += 1
        data=self.q[self.front]
        self.q[self.front]=0
        return data

q=queue()
q.enqueue(1)
q.enqueue(2)
print(q.dequeue())
print(q.dequeue())
q.enqueue(1)
print(q.dequeue())
```



**위의 방식으로 사용하면 enqueue()와 dequeue()가 반복하는 과정에서 큐가 차지하는 메모리가 계속해서 커질 수 있고, 그만큼 메모리 낭비가 심해진다.**



**그러한 단점을 보완하기 위해 고안해낸 것이 원형큐이다. 원형큐는 큐의 사이즈를 정해놓고 모듈러 연산(%)을 통해 무기한으로 커질 수 있는 큐의 크기와 front,rear를 제한시켜 메모리를 효율적으로 사용할 수 있다.**



**[참고]**

- https://gyoogle.dev/blog/computer-science/data-structure/Stack%20&%20Queue.html