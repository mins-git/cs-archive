# [운영체제] Chapter 5. CPU Scheduling

---

## 1. 프로그램 실행과 CPU/IO Burst

모든 프로그램은 실행 시 **CPU Burst**와 **I/O Burst**의 연속으로 구성됩니다.

* **CPU Burst**: 프로세스가 CPU를 잡고 명령어를 실행하는 단계 (연산, 제어 등)
* **I/O Burst**: 프로세스가 커널에 I/O를 요청한 후 결과가 나올 때까지 대기하는 단계 (디스크 읽기/쓰기, 네트워크 통신 등)

### CPU-Burst Time의 분포
프로그램의 종류에 따라 CPU burst와 I/O burst의 비율이 크게 달라집니다.

* **I/O-bound Process**: CPU를 짧게 사용하고 I/O를 빈번하게 수행하는 프로세스 (주로 대화형 프로그램, Interactive Job)
* **CPU-bound Process**: 주로 계산 작업을 많이 하여 CPU를 길게 사용하는 프로세스 (주로 연산 중심 프로그램)

> **CPU 스케줄링의 필요성**: 여러 종류의 프로세스가 섞여 있기 때문에 CPU를 효율적으로 나누어 주어야 합니다. 특히 인간과 상호작용하는 **I/O-bound job에게 CPU를 우선적으로 적절히 배분**해야 사용자 경험을 극대화할 수 있습니다.

---

## 2. CPU Scheduler & Dispatcher

### CPU Scheduler
* 메모리의 **Ready Queue**에 있는 프로세스들 중 어떤 프로세스에게 CPU를 할당할지 결정하는 **운영체제 커널의 코드**입니다.

### Dispatcher
* CPU 스케줄러가 선택한 프로세스에게 **실제로 CPU의 제어권을 넘겨주는 커널의 코드**입니다.
* 이 과정에서 **Context Switch(문맥 교환)**가 발생합니다.

### 비선점형 vs 선점형 스케줄링
1. **비선점형(Non-preemptive)**: 강제로 CPU를 빼앗지 않고, 프로세스가 스스로 CPU를 반납할 때까지 기다리는 방식.
2. **선점형(Preemptive)**: 운영체제가 강제로 CPU를 빼앗을 수 있는 방식. 현대 OS는 대부분 선점형을 채택하고 있습니다.

---

## 3. 스케줄링 성능 척도 (Scheduling Criteria)

* **시스템 관점**: CPU Utilization (이용률), Throughput (처리량) - 최대화
* **사용자 관점**: Turnaround Time (소요 시간), Waiting Time (대기 시간), Response Time (응답 시간) - 최소화

---

## 4. 단일 큐 스케줄링 알고리즘 (Scheduling Algorithms)

### (1) FCFS (First-Come First-Served)
* **개념**: 먼저 도착한 프로세스를 먼저 처리하는 비선점형 방식.
    - 식당에 도착한 순서대로 요리를 해주는 방식임.
* **문제점 (Convoy Effect)**: CPU burst가 긴 프로세스가 앞에 도착하면, 뒤에 있는 짧은 프로세스들의 대기 시간이 급격히 늘어나는 현상.

### (2) SJF (Shortest-Job-First)
* **개념**: CPU burst time이 가장 짧은 프로세스에게 CPU를 먼저 할당하는 방식.
    - 주문 들어온 것 중 가장 금방 만들 수 있는 요리 부터 먼저 처리하는 방식(대기 시간을 줄일 수 있음.)
* **장점**: 평균 대기 시간을 최소화하는 최적 알고리즘.
* **단점**: Starvation(기아 현상) 발생 가능, CPU Burst Time의 예측 불가능성(Exponential Averaging으로 예측).

### (3) Priority Scheduling (우선순위 스케줄링)
* **개념**: 가장 높은 우선순위를 가진 프로세스에게 CPU를 할당.
* **해결책 (Aging)**: Ready Queue에서 기다린 시간에 비례하여 프로세스의 우선순위를 점진적으로 높여주어 기아 현상을 방지.

### (4) Round Robin (RR)
* **개념**: 각 프로세스는 동일한 크기의 할당 시간(Time Quantum)을 가짐. 할당 시간이 지나면 선점당하고 Ready Queue의 맨 뒤로 이동.
   - 현대 컴퓨터가 많이 쓰는 방식으로 주방장이 타이머를 맞추고 1분동안 A 테이블 요리를 하다가 미완성이어도 B테이블로 요리를 1분하고 그다음 c를하는 방식.
* **특징**: Response Time이 매우 짧아짐. 할당 시간이 너무 크면 FCFS와 같아지고, 너무 작으면 Context Switch 오버헤드가 커짐.

---

## 5. 다단계 큐 및 특수 스케줄링 알고리즘

### (1) Multilevel Queue (다단계 큐)
* Ready Queue를 여러 개로 분할 (예: Foreground - RR, Background - FCFS).

### (2) Multilevel Feedback Queue (MLFQ)
* 프로세스가 다른 큐로 이동할 수 있는 방식. 연산이 길어지면 하위 큐로 강등되어 I/O bound process를 우대함.

### (3) Multi-Processor Scheduling
* 여러 개의 CPU가 있는 환경의 스케줄링 (Load Balancing, Processor Affinity 등 고려).

### (4) Real-Time Scheduling
* 정해진 Deadline 내에 반드시 작업이 완료되어야 하는 환경 (Hard / Soft Real-time).

### (5) Thread Scheduling
* Local Scheduling (유저 레벨) vs Global Scheduling (커널 레벨).