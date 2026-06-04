# [운영체제] Chapter 6. Process Synchronization
---

## 1. 데이터의 접근과 Race Condition

### Race Condition (경쟁 상태)
여러 주체(Process/Thread)가 **공유 데이터(Shared Data)에 동시에 접근**하여 조작할 때, 접근 순서에 따라 실행 결과가 달라지는 현상을 의미합니다.

---

## 2. 운영체제(OS Kernel)에서의 Race Condition 상황

1. **커널 모드 수행 중 인터럽트 발생 시**: 인터럽트 Disable/Enable로 해결.
2. **프로세스가 커널 모드 실행 중 문맥 교환 발생 시**: 커널 모드 수행 중에는 CPU 선점을 방지(Preempt disable)하여 해결.
3. **Multiprocessor 시스템에서 공유 커널 데이터 접근 시**: 개별 데이터에 Lock/Unlock 적용.

---

## 3. 임계 구역 문제 (The Critical-Section Problem)

* **Critical Section(임계 구역)**: 공유 데이터에 접근하는 코드의 구역.

### 해결 조건 3가지
1. **Mutual Exclusion (상호 배제)**: 한 프로세스가 임계 구역에 있으면 다른 프로세스는 진입 불가.
2. **Progress (진행)**: 임계 구역이 비어있을 때 진입을 원하는 프로세스가 있다면 진입하게 해주어야 함.
3. **Bounded Waiting (유한 대기)**: 진입 요청 후 허가될 때까지의 대기 횟수에 한계가 있어야 함 (Starvation 방지).

---

## 4. 초기 소프트웨어적 해결 알고리즘

* **Algorithm 1 (Turn)**: Progress 조건 위반.
* **Algorithm 2 (Flag)**: Progress 조건 위반.
* **Algorithm 3 (Peterson's Algorithm)**: Turn과 Flag 혼합. 3가지 조건 모두 만족하나 **Busy Waiting(Spin Lock)** 문제 발생.

---

## 5. 하드웨어적 동기화 지원

* **TestAndSet 명령어**: 읽기와 쓰기를 하나의 원자적(Atomic) 명령어로 처리하여 동기화 문제를 간단히 해결.

---

## 6. 세마포어 (Semaphores)

정수 값과 두 가지 원자적 연산 **P(S)**와 **V(S)**로만 접근 가능한 추상 자료형.

* **P(S)**: 자원 획득 연산 (S가 0 이하면 대기, 양수면 감소)
* **V(S)**: 자원 반납 연산 (S를 증가)

### Busy-wait vs Block/Wakeup
* **Busy-wait (Spin Lock)**: 자원이 없으면 루프를 돌며 대기 (CPU 낭비).
* **Block/Wakeup (Sleep Lock)**: 자원이 없으면 프로세스를 대기 큐(Blocked)에 넣고, 자원이 생기면 깨움(Wakeup). 임계 구역이 길 때 효율적.

---

## 7. 동기화로 인해 발생하는 문제점들

* **Deadlock (교착 상태)**: 둘 이상의 프로세스가 서로 상대방의 자원을 기다리며 무한 대기.
* **Starvation (기아 현상)**: 특정 프로세스가 자원을 무한히 얻지 못하는 상태.

---

## 8. 전통적인 동기화 문제들

1. **Bounded-Buffer Problem (생산자-소비자 문제)**: 빈 칸과 채워진 칸의 개수를 세마포어로 관리.
2. **Readers-Writers Problem (독자-저자 문제)**: Reader는 동시 접근 허용, Writer는 독점 접근.
3. **Dining-Philosophers Problem (식사하는 철학자 문제)**: 교착 상태를 막기 위해 양쪽 젓가락을 모두 잡을 수 있을 때만 집도록 제한.

---

## 9. 모니터 (Monitors)

### 세마포어의 한계
* 코딩이 어렵고 한 번의 실수가 치명적임 (예: P와 V의 순서 오류).

### 모니터의 개념
* 프로그래머에게 상호 배제를 자동 보장해 주는 **고수준 동기화 구조**.
* 모니터 내부의 프로시저(함수)를 통해서만 공유 데이터에 접근 가능.
* **조건 변수 (Condition Variable)**: `wait()`와 `signal()`을 사용하여 프로세스를 잠재우거나 깨우는 것을 정밀하게 제어.