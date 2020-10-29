# Performance

> 2020.10.29



## 1. Measuring Computer Performance

> 컴퓨터의 성능을 측정하기 위한 단위



### 1.1 Response Time

- Execution time, latency로도 불리며, 작업의 시작부터 종료까지 걸린 시간을 의미한다.
- 일반 컴퓨터와 임베디드 컴퓨터는 response time에 중점을 둔다.



### 1.2 Throughput

- 주어진 시간 당 처리하는 작업의 총량을 의미한다.
- 서버를 다루는 데이터 센터나 슈퍼컴퓨터들은 throughput에 중점을 둔다.



### 1.3 Pipeline

- 파이프라인은 한 데이터 처리 단계의 출력이 다음 단계의 입력으로 이어지는 형태로 연결된 구조를 가리킨다. 이렇게 연결된 데이터 처리 단계는 한 여러 단계가 서로 동시에, 또는 병렬적으로 수행될 수 있어 효율성의 향상을 꾀할 수 있다. 

- 파이프라인은 latency(response time)에는 영향을 미치지 않고, throughput에 영향을 미친다. 



### 1.4 Relative Performance

- 컴퓨터의 성능을 최대화하기 위해서는, 작업의 실행 시간을 최소화해야 한다.
- 그렇기 때문에, **한 컴퓨터의 performance는 1/executionTime**으로 수치화 할 수 있다.
- **execution time**은 disk access, memory access, I/O activities, OS overhead 모두를 포함한다.
- **CPU Time** : 주어진 task를 처리하는데까지 CPU가 사용된 시간으로, 다른 프로그램을 실행하거나, I/O를 기다린 시간은 포함하지 않는다.





**[참고]**

- https://ko.wikipedia.org/wiki/%ED%8C%8C%EC%9D%B4%ED%94%84%EB%9D%BC%EC%9D%B8_(%EC%BB%B4%ED%93%A8%ED%8C%85)