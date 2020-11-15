# Heap

> 2020.11.15



#### 힙

> 완전 이진 트리의 일종으로 여러 값 중 최대값과 최소값을 빠르게 찾도록 만들어진 자료구조이다.(힙은 중복값을 허용한다.)



- 최대힙 : 부모 노드의 키 값이 자식 노드의 키 값보다 크거나 같은 완전이진트리
- 최소힙 : 부모 노드의 키 값이 자식 노드의 키 값보다 작거나 같은 완전이진트리

- 부모 노드와 자식 노드와의 관계
  - 왼쪽 자식 : (부모 index)  * 2
  - 오른쪽 자식 : (부모 index) * 2 + 1
  - 부모 : (자식 index) // 2



**구현**

```python
class MaxHeap():
    def __init__(self):
        self.h=[]

    def push(self,data):
        self.h.append(data)
        idx=len(self.h)-1
        while idx>=0:
            p_idx=(idx-1)//2
            if p_idx>=0 and self.h[idx]>self.h[p_idx]:
                self.h[idx],self.h[p_idx]=self.h[p_idx],self.h[idx]
                idx=p_idx
            else:
                break

    def pop(self):
        self.h[0],self.h[-1]=self.h[-1],self.h[0]
        max_res=self.h.pop(-1)
        idx=0
        while idx<len(self.h):
            l,r=(idx*2)+1,(idx*2)+2
            max_idx=idx
            if l<len(self.h) and self.h[max_idx]<self.h[l]:
                max_idx=l
            if r<len(self.h) and self.h[max_idx]<self.h[r]:
                max_idx=r
            if idx==max_idx:
                break
            self.h[idx],self.h[max_idx]=self.h[max_idx],self.h[idx]
            idx=max_idx
        return max_res

h=MaxHeap()
h.push(1)
h.push(3)
h.push(11)
h.push(6)
h.push(5)
h.push(2)
print(h.pop())
print(h.pop())
print(h.pop())
print(h.pop())
print(h.pop())
print(h.pop())
```



**[참고]**

- https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/DataStructure
- https://gyoogle.dev/blog/computer-science/data-structure/Heap.html
- https://daimhada.tistory.com/108