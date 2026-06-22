# CS Archive

> 컴퓨터 과학(CS) 핵심 개념 및 시스템 아키텍처 학습 보관소. 
> 표면적인 암기가 아닌, 시스템의 동작 원리와 '왜(Why)'를 중심으로 체계적으로 기록합니다.

<br>

## 🗂️ Index

현재 진행 중인 학습과 앞으로 확장해 나갈 지식의 목차입니다.

- [Operating System](./Operating-System) ✅ 진행 중
- [Network](./Network)
- [Database](./Database)
- [Data Structure & Algorithm](./Data-Structure-Algorithm)
- [Java](./Java)
- [Spring](./Spring)
- [TIL](./TIL) 🌱 프로젝트 진행 중 학습 기록


<br>

## 📚 Study Tracker

### 🖥️ Operating System
핵심 동작 원리와 백엔드 개발에 필요한 시스템 기반 지식을 정리합니다.

- [ ] **01. Introduction to Operating Systems** (강의 소개)
  - 운영체제의 목적, 분류, 구조
- [ ] **02. System Structure & Program Execution** (시스템 구조와 프로그램 실행)
  - Mode bit, Timer, Device Controller, 동기식/비동기식 입출력
  - 인터럽트(Interrupt), 시스템 콜(System Call), DMA
- [ ] **03. Process** (프로세스)
  - 프로세스 상태(State), PCB, 문맥 교환(Context Switch)
  - 스케줄러(Scheduler), 스레드(Thread)의 개념과 구현
- [ ] **04. Process Management** (프로세스 관리)
  - 프로세스 생성 및 종료, IPC (Interprocess Communication)
  - CPU & I/O Bursts
- [ ] **05. CPU Scheduling** (CPU 스케줄링)
  - FCFS, SJF, Priority, Round Robin(RR), Multilevel Queue
  - CPU 스케줄러와 디스패처(Dispatcher)
- [ ] **06. Process Synchronization** (프로세스 동기화)
  - Race Condition, Critical-Section Problem
  - 뮤텍스(Mutex), 세마포어(Semaphores), 모니터(Monitor)
  - 식사하는 철학자 문제 (Dining-Philosophers)
- [ ] **07. Deadlocks** (교착 상태)
  - 발생 4가지 조건, 자원 할당 그래프
  - 예방(Prevention), 회피(Avoidance), 은행원 알고리즘(Banker's Algorithm)
- [ ] **08. Memory Management** (메모리 관리)
  - Logical vs Physical Address, 주소 바인딩, MMU
  - 페이징(Paging), 세그먼테이션(Segmentation), TLB
- [ ] **09. Virtual Memory** (가상 메모리)
  - Demand Paging, Page Fault, 캐싱 환경
  - 페이지 교체 알고리즘 (Optimal, FIFO, LRU, LFU, Clock)
  - 스레싱(Thrashing), Working-Set Model
- [ ] **10. File Systems & Implementation** (파일 시스템)
  - 디렉토리 논리적 디스크, 접근 방식
  - 파일 데이터 할당 (Contiguous, Linked, Indexed)
  - VFS/NFS, Page Cache, Buffer Cache
- [ ] **11. Disk Management and Scheduling** (디스크 관리 및 스케줄링)
  - 디스크 스케줄링 (FCFS, SSTF, SCAN, C-SCAN)
  - Swap-Space Management, RAID

<br>

---

### 🌱 TIL (Today I Learned)
프로젝트 개발 및 학습 과정에서 배운 것을 날마다 기록합니다.

| 날짜 | 내용 |
|------|------|
| 2026-06-22 | 프로젝트 세팅, Spring Boot 의존성 구성 |

<br>

---

## ✍️ Record Rule

문서를 작성할 때 유지하는 개인적인 원칙입니다.

1. **Keep it Simple:** 불필요한 미사여구는 배제하고 핵심 논리와 메커니즘을 간결하게 서술한다.
2. **Context First:** 기술이 등장한 배경과 '해결하고자 했던 문제'를 먼저 명시한다.
3. **Reference:** 외부 자료나 공식 문서를 참고한 경우 반드시 출처를 하단에 남긴다.

---
*Last Updated: 2026. 06. 22*
