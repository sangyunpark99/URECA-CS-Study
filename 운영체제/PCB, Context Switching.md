# PCB

## 1) PCB란? 

- 프로세스 관리 블록으로, OS가 프로세스 관리에 필요한 정보를 저장한 구조체
- 프로세스 생성 시 커널에 PCB 생성

> 💡 **PCB가 저장되는 위치**
> PCB는 일반 사용자가 접근할 수 없는 메모리의 특수한 부분에 저장된다. 이는 프로세스에 대한 중요한 정보를 보관하기 때문이다. 일부 운영 체제는 PCB를 프로세스의 커널 스택 시작 부분에 배치하는데, 이는 안전하고 보안이 유지되는 지점이기 때문이다.

<br>

## 2) PCB에 저장되는 정보

- 프로세스 식별자 (PID) : 프로세스 식별 번호
- 프로세스 상태 : new, ready, running, waiting, terminated 등의 상태 저장
- 프로그램 카운터 : 프로세스가 다음에 실행할 명령어의 주소
- CPU 레지스터 : CPU에서 사용한 레지스터의 값을 잃지 않기 위해 PCB에 그 값 저장
- CPU 스케줄링 정보 : 프로세스의 우선순위, 스케줄 큐에 대한 포인터 등
- 메모리 관리 정보 : 페이지 테이블 또는 세그먼트 테이블 등과 같은 정보 포함
- 입출력 상태 정보 : 프로세스에 할당된 입출력 장치들과 열린 파일 목록

<br>

## 3) PCB가 필요한 이유

- CPU에서는 프로세스 상태에 따라 교체작업이 이루어지는데, 이때 앞으로 수행할 대기 중인 프로세스에 관한 값을 PCB에 저장해두는 것
- 즉, 프로세스의 상태 관리와 Context Switching을 위해 필요

<br>

## 4) PCB 관리 방식

- LinkedList 방식으로 관리
- PCB List Head에 PCB들이 생성될 때마다 붙게 됨. 
- 주소값으로 연결이 이루어져 있는 연결리스트이기에 삽입/삭제가 용이함
- 프로세스 생성되면 PCB가 생성되고 프로세스 완료되면 PCB가 제거됨

<br><br>

---
# Context Switching

## 1) Context Switching이란?

- CPU를 한 프로세스/스레드에서 다른 프로세스/스레드로 넘겨주는 과정
	- 이때, CPU가 해당 프로세스를 실행하기 위한 정보들을 Context라고 함
- 실행 중인 프로세스의 Context를 저장하고 앞으로 실행할 프로세스의 Context를 복구하는 일
- 커널의 개입으로 이루어짐
- 여러 프로세스/스레드를 동시에 실행시키기 위해 필요


>❗️**Context Switching이 아닌 경우 구분**
>시스템 콜이나 인터럽트 발생시 항상 문맥교환이 일어나는 것은 아니다. 
>- Timer Interrupt처럼 시스템 콜에 의해 운영체제가 다른 사용자 시스템에게 CPU를 넘긴다면, 문맥 교환이 맞다.
>- 발생 이전의 프로세스한테 다시 CPU를 넘기는 것은 문맥교환이 아니다. 
>물론 발생 이전의 프로세스에게 다시 넘기는 경우도 context의 일부를 PCB에 저장해야 한다. 하지만 전자에 비해 그 부담이 훨씬 적다. 

<br>

## 2) Context Switching 발생 원인

Ready -> Running, Running -> Ready, Running -> Waiting처럼 상태 변경 시 발생

1. Interrupt handling
	- 커널 함수를 통해 프로그램 실행 도중 중단되어 인터럽트 처리를 기다리는 경우
	
2. Multitasking
	- 단일 CPU에서 동시에 작업이 실행되는 것처럼 보이도록 하는 경우 (동시성은 Context Switching을 통해 달성됨)
		- Time Quantum Expiry : 주어진 Quantum의 시간이 끝난 경우 (CPU 사용 시간이 만료되었을 때)
		- Preemption : 더 우선순위가 높은 일을 해야하는 경우
	
3. 사용자 및 커널 모드 전환
	- 필수는 아니지만 운영체제에 따라 발생 가능

<br>

## 3) Context Switching 과정
### 3-1) 기본 작업

- 커널 모드로 전환
- CPU register 상태 교체

### 3-2) 작동 순서

상황 : 프로세스 A가 running 상태이고, 프로세스 B가 ready 상태일 때

1. 스케줄러가 프로세스 A의 실행을 중단하고 프로세스 B를 실행할 것을 요청함 
2. 프로세스 A의 Stack의 데이터 위치를 가리키고 있는 SP(Stack Pointer)의 값과 다음 실행해야 하는 코드의 주소값을 가지고 있는 PC(Program Counter)의 값을 PCB에 업데이트한 후에 메인 메모리에 저장함
3. 프로세스 A의 상태는 ready 혹은 blocked 상태로 변경되고, CPU에서 프로세스 B를 실행함. 이 과정에서 프로세스 B의 상태는 ready에서 running으로 변경됨 (dispatch)
4. 그리고 다시 프로세스 B에서 프로세스 A로 Context Switching 하는 경우, 프로세스 B의 SP값과 PC값을 PCB에 저장함
5. 이후, 실행해야할 프로세스 A의 PCB 정보들을 메인 메모리에서 가져와서 CPU 레지스터에 넣고 실행함
<br>

## 4) Context Switching 오버헤드

- Context Switching 오버헤드 : 문맥교환에 소요되는 시간과 메모리
- Context Switching은 ms의 짧은 시간 단위로 일어나지만, 과도하게 많이 일어나면 오버헤드가 발생함
- 오버헤드를 감수하면서 Context Switching을 하는 이유
	- I/O 이벤트가 발생했을 때, 해당 이벤트가 끝날 때까지 기다리면 CPU를 점유하고 있어도 아무런 작업도 할 수 없기 때문에 CPU가 낭비된다. 때문에 오버헤드를 감수하면서 기존 프로세스를 새 프로세스로 바꾸는 것이 더 효율적이다.
	- 멀티태스킹에서 시간 할당량이 적어지면 문맥 교환의 수와 오버헤드가 증가하지만 동시에 더 많은 프로세스를 수행할 수 있고, 시간 할당량이 커지면 문맥 교환의 수와 오버헤드는 감소하지만 더 적은 프로세스를 동시에 수행할 수 있다. 


## 5) 프로세스와 스레드에서의 Context Switching

둘의 공통점은 커널 모드에서 실행된다는 점

### 5-1) Process Context Switching

- 작업 : 커널 모드 전환 + CPU register 상태 교체 + 가상  메모리 주소 처리 (MMU 수정 + TLB 캐시 비우기)
- 현재 실행중인 프로세스의 스레드와는 다른 프로세스의 스레드와 Context Switching이 발생하는 것
- 캐시 오염 (cache pollution) 발생
	- CPU 내부에 캐시를 위한 공간이 존재하는데, Context Switching이 발생하면 캐시의 데이터가 현재 실행중인 스레드의 데이터와 다를 수 있음
	- 프로세스가 변경되어 새로운 프로세스가 CPU를 사용하지만, 캐시에는 이전 프로세스에서 사용하던 전혀 다른 데이터에 대한 캐시가 남게 되는데 이를 캐시 오염이라고 함
	- 그나마 같은 프로세스에 속한 쓰레드 간 Context Switching일 경우에는 유의미한 캐시 데이터가 있을 가능성이 조금 더 있을 순 있음
- 가상 메모리 주소 관련 처리를 추가로 수행해야 함
	- MMU(Memory Management Unit)가 새로운 프로세스의 주소 체계를 바라보도록 수정함
	- 캐시 역할을 하는 TLB(Translation Lookaside Buffer)를 완전히 비워줘야함


### 5-2) Thread Context Switching

- 작업 : 커널 모드 전환 + CPU register 상태 교체
- 같은 프로세스 안의 스레드끼리 Context Switching이 발생하는 것
- 스레드는 스택 영역을 제외한 모든 메모리 영역을 공유하기 때문에 메모리 주소 관련한 정보는 바꿀 필요가 없고, CPU의 상태정보만 바꿔주면됨
	- 따라서 Thread Context Switching은 공유하는 정보가 많아 기본 작업만 하면 되기 때문에 Process Context Switching보다 더 빠름