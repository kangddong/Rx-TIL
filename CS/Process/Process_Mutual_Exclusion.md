

# 상호배제 (Mutual Exclusion)

공유자원을 한 시점에 단지 하나의 프로세스만이 사용할 수 있도록 제어하는 매커니즘

# 임계 구역(critical section)


## 소프트웨어적 기법

### 뮤텍스

1. 데커 알고리즘 (Dekker's algorithm)
2. 피터슨 알고리즘 (Peterson's algorithm)
3. 다익스트라 알고리즘 (Dijkstra algorithm)
4. 제과점 알고리즘 (Bakery's algorithm)

### 세마포어
### 모니터
### 스핀락

critical section problem 동시성 문제

1. Race condition (경쟁상황)
2. Deadlocks (교착상태)
3. Priority Inversion (우선 순위의 뒤바뀜)