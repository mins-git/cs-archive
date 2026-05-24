# 면접 Q&A
---
# 1. Device Controller

## Q1.
Device Controller는 CPU처럼 범용 연산을 수행할 수 있나요?

---

## A1.

불가능합니다.

Device Controller는 CPU처럼 보일 수 있지만,
실제 CPU처럼 범용 연산을 수행하는 장치는 아닙니다.

정확히는 특정 I/O 장치를 제어하기 위한 전용 제어기입니다.

내부에 간단한 프로세서(마이크로컨트롤러)나 펌웨어가 들어있는 경우가 많지만,
목적이 제한되어 있습니다.

즉:
- CPU → 범용 연산 수행
- Device Controller → 특정 장치 제어 전용

이라는 차이가 있습니다.

---

## 예시

- SSD Controller
  - 플래시 메모리 관리
  - wear leveling
  - garbage collection 수행

- GPU 내부 Controller
  - 그래픽 작업 스케줄링

- NIC(Network Interface Card)
  - 네트워크 패킷 처리 일부 수행

---

## 추가 꼬리 질문

### Q.
그렇다면 왜 Device Controller가 필요한가요?

### A.
CPU가 모든 I/O 장치를 직접 제어하면 부담이 매우 커지기 때문입니다.

따라서 Device Controller가:
- 장치와의 세부 통신 처리
- 데이터 버퍼 관리
- interrupt 발생

등을 대신 수행하여 CPU 부담을 줄여줍니다.

---

# 2. Timer Interrupt

## Q2.
무한 루프를 실행 중인 프로세스가 있다고 가정하겠습니다.

```c
while(true) {
    x++;
}
```

이 상황에서 Timer interrupt가 발생하여 CPU 제어권을 OS가 회수했습니다.

이후 다시 해당 프로세스가 스케줄링되면,
while문의 처음부터 다시 실행되나요?
아니면 interrupt가 걸렸던 지점부터 이어서 실행되나요?

---

## A2.

interrupt가 걸렸던 정확한 지점부터 이어서 실행됩니다.

운영체제는 Timer interrupt 발생 시 현재 프로세스의 실행 상태를 저장합니다.

예를 들면:
- Program Counter(PC)
- Register 값
- Stack Pointer
- CPU 상태 정보

등을 PCB(Process Control Block)에 저장합니다.

따라서 다시 스케줄링되면,
while문의 처음부터 실행되는 것이 아니라,

interrupt가 발생했던 CPU 명령 다음 위치부터 실행을 재개합니다.

즉 Timer interrupt는:
- 프로세스를 종료시키는 것이 아니라
- 실행을 잠시 중단(preemption)시키는 것입니다.

---

## 추가 꼬리 질문

### Q.
Timer interrupt가 없다면 어떤 문제가 발생하나요?

### A.
특정 프로세스가 CPU를 계속 점유할 수 있게 됩니다.

예를 들어 무한 루프 프로그램이 실행되면:
- OS가 CPU 제어권을 회수하지 못함
- 다른 프로세스 실행 불가능
- 멀티태스킹 불가능

상태가 될 수 있습니다.

따라서 Timer interrupt는
OS가 CPU 제어권을 강제로 회수할 수 있도록 해주는 핵심 장치입니다.