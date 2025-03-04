## 신예지

<details> 
<summary><b>PCB에는 parent PID도 저장이 됩니다. 왜 부모의 PID가 자식의 PCB에 저장될까요?</b></summary>
<div markdown="1">

자식 프로세스가 종료될 경우 부모 프로세스에게 알리기 위해 부모의 PID를 저장합니다. 이를 통해 부모 프로세스는 자식 프로세스의 종료 상태를 확인하고 적절한 후처리를 할 수 있습니다.

</div>
</details>

<details>
<summary><b>control stack이 존재하는 위치와 control stack의 역할을 설명해주세요</b></summary>
<div markdown="1">

control stack은 프로세스 이미지 중 kernel stack에 위치하고, CPU의 상태(Processor State Information)를 저장하고 복원하는 역할을 합니다. Context Switching 시 현재 프로세스의 레지스터 값, PC, SP 등의 중요한 상태 정보를 저장하고 새로운 프로세스의 상태로 복원합니다.

</div>
</details>

<details>
<summary><b>Context Swtiching이 발생하는 경우 4가지를 말해주세요</b></summary>
<div markdown="1">

- CPU 스케줄링에 의해 프로세스 전환
- 인터럽트(Interrupt) 발생
- 시스템 콜(System Call) 실행
- 멀티스레딩 환경에서 스레드 전환

</div>
</details>

<details>
<summary><b>Context Switching 과정에서 왜 PC(Program Counter)와 SP(Stack Pointer)를 가장 먼저 저장해야 할까요?</b></summary>
<div markdown="1">

PC는 현재 실행 중인 명령어의 주소를 가지고 있고, 스택 포인터는 현재의 함수 호출 스택을 가리키는 위치를 저장합니다. 스택에는 함수의 지역 변수, 반환 주소, 호출된 함수의 매개변수 등 중요한 정보들이 들어 있습니다.
Context Switching 시에 프로그램 카운터와 스택 포인터를 저장하지 않으면 현재 실행 중인 명령어의 주소와 함수 호출 스택의 위치를 잃어버려 다시 해당 작업으로 돌아왔을 때 제대로 상태를 복구할 수 없게 됩니다. 그 결과 다시 그 작업으로 돌아왔을 때 어디서부터 실행을 계속해야 할지 알 수 없게 됩니다.

</div>
</details>

<details>
<summary><b>Context Switching 과정에서 발생하는 캐시 오염(Cahce Pollution)에 대해 설명해주세요</b></summary>
<div markdown="1">

캐시 오염이란 프로세스 간의 Context Switching이 발생하면서 캐시에 이전에 실행하던 프로세스의 데이터가 남아 현재 프로세스에서 캐시를 효과적으로 사용할 수 없는 현상을 말합니다. 이로 인해 캐시 적중률이 떨어지고 성능 저하가 발생할 수 있습니다.
CPU의 캐시 메모리는 실행 중인 프로세스의 데이터를 저장하는데, Context Switching이 발생하면 기존 프로세스의 데이터가 캐시에서 제거되고 새로운 프로세스의 데이터가 로드됨. 하지만 이전 프로세스로 다시 전환되면 캐시에 필요한 데이터가 없기 때문에 성능 저하(캐시 미스)가 발생함.

</div>
</details>

<details>
<summary><b>Thread Context Switching 과 Process Context Switching의 차이점에 대해 설명해주세요</b></summary>
<div markdown="1">

### 1. **Context Switching의 대상**
- **Process Context Switching**: 프로세스 간 전환을 의미합니다. 하나의 프로세스에서 다른 프로세스로 전환될 때 발생합니다. 프로세스는 독립된 실행 단위로, 각 프로세스는 자체 메모리 공간과 자원을 가지고 있습니다.
- **Thread Context Switching**: 동일한 프로세스 내에서 스레드 간 전환을 의미합니다. 스레드는 프로세스 내의 실행 단위로, 같은 메모리 공간을 공유합니다. 스레드 간 전환은 같은 프로세스 내에서 이루어집니다.

### 2. **저장해야 하는 정보**
- **Process Context Switching**: 프로그램 카운터(PC), 스택 포인터(SP), 일반 레지스터, CPU 상태 등 모든 프로세스 상태 정보뿐만 아니라 프로세스의 메모리 맵핑 정보도 저장 및 복원해야 합니다.
- **Thread Context Switching**: 프로그램 카운터(PC), 스택 포인터(SP), 레지스터 등 스레드별 상태 정보만 저장 및 복원하면 됩니다. 스레드 컨텍스트 스위칭에서는 같은 주소 공간을 공유하므로 메모리 매핑 정보 변경이 필요 없습니다.

### 3. **전환의 비용**
- **Process Context Switching**: 메모리 공간 및 자원을 모두 변경해야 하므로 더 많은 오버헤드가 발생합니다. 메모리 캐시와 TLB(Translation Lookaside Buffer)도 무효화되어 성능에 영향을 미칠 수 있습니다.
- **Thread Context Switching**: 같은 메모리 공간을 공유하므로 상대적으로 전환 비용이 적습니다. 캐시와 TLB 무효화가 필요하지 않아 성능 저하가 상대적으로 적습니다.

### 4. **오버헤드**
- **Process Context Switching**: 프로세스 간의 자원 변경 때문에 더 큰 오버헤드가 발생합니다.
- **Thread Context Switching**: 적은 오버헤드로 신속한 전환이 가능합니다.

</div>
</details>

---

## 이소원

<details> 
<summary><b>컨텍스트 스위칭을 과도하게 하면 어떤 문제가 발생할까요?</b></summary>
<div markdown="1">

성능이 저하됩니다.

- **CPU 오버헤드 증가** → 문맥 교환 과정 자체가 CPU 자원을 소비
- **캐시 오염(Cache Pollution) 발생** → 캐시를 자주 비우면서 성능 저하
- **실제 작업보다 문맥 교환에 더 많은 시간을 소비**

</div>
</details>

<details> 
<summary><b>시스템 성능을 고려할 때, 문맥 교환이 잦아지는 상황을 어떻게 최적화할 수 있을까요?</b></summary>
<div markdown="1">

- **적절한 타임 슬라이스 조정**
    - 너무 짧으면 문맥 교환이 잦아져 오버헤드 증가
    - 너무 길면 응답성이 떨어짐 → 적절한 값으로 조정
- **캐시 친화적인 스케줄링**
    - 동일한 코어에서 동일한 프로세스를 계속 실행하도록 하여 캐시 오염 최소화
- **멀티스레딩 활용**
    - 같은 프로세스 내에서 컨텍스트 스위칭을 하면 비용이 줄어듦

</div>
</details>

<details> 
<summary><b>프로세스 간 문맥 교환과 스레드 간 문맥 교환에서 스레드 문맥 교환이 더 빠른 이유가 뭘까요?</b></summary>
<div markdown="1">

스레드는 같은 프로세스 내에서 공유하는 메모리가 많아 필요한 변경 작업이 적기 때문에 더 빠릅니다.

</div>
</details>

<details> 
<summary><b>PCB를 효율적으로 관리하는 방법에는 어떤 것들이 있을까요?</b></summary>
<div markdown="1">

- 필요한 정보만 저장하고 불필요한 데이터를 줄일 수 있습니다.
- 프로세스 상태 최적화 (ex. Ready 상태에서 대기 중인 프로세스를 효과적으로 관리)
- 멀티코어 환경에서 문맥 교환을 줄이기 위한 최적화 기법 적용
- PCB를 캐싱하여 접근 속도를 높임 (TLB, 캐시 사용)

</div>
</details>

<details> 
<summary><b>왜 오버헤드를 감수하면서까지 문맥 교환을 해야 할까요?</b></summary>
<div markdown="1">

- 상황 1. I/O 이벤트가 발생할 때 CPU 낭비를 줄이기 위해
    
    입출력 이벤트가 끝날 때까지 기다리면 CPU는 점유되고 있지만 아무런 작업도 하지 않아 CPU가 낭비되는 상황이 발생한다. 따라서 오버헤드를 감수하면서 기존 프로세스를 새 프로세스로 바꾸는 것이 더 효율적이다.
    
- 상황 2. 멀티 태스킹을 가능하게 하기 위해
    
    시간 할당량이 적어지면 문맥 교환과 오버 헤드가 증가하지만 동시에 더 많은 프로세스를 수행할 수 있고, 시간 할당량이 커지면 문맥 교환의 수와 오버헤드는 감소하지만 더 적은 프로세스를 동시에 수행할 수 있습니다.

</div>
</details>

<details> 
<summary><b>언제 context switching 이 발생하나요?</b></summary>
<div markdown="1">

1. Interrupt handling : 커널 함수를 통해 프로그램 실행 도중에 중단되어 인터럽트 처리를 기다리는 경우
2. Multitasking : 단일 cpu에서 동시에 작업이 실행된느 것처럼 보이도록 하는 경우 (동시성은 컨텍스트 스위칭을 통해 달성된다.)
    - 타임 퀀텀 종료 (Time Quato Expiry) : 주어진 quantum(time slice)의 시간이 끝난 경우(CPU의 사용 시간이 만료되었을 때
    - 선점 (Preemption) : 더 우선순위가 높은 일을 해야하는 경우
3. 사용자 및 커널 모드 전환 시
    - 시스템 호출(SYS_CALL)이나 예외(Exception) 발생 시
    - 실행 중이던 프로세스가 커널 모드에서 실행되는 다른 프로세스로 전환될 수 있습니다.

</div>
</details>

<details> 
<summary><b>프로세스 관련 정보는 실행 상태에 따라 어느 곳에 저장되나요?</b></summary>
<div markdown="1">

메인 메모리(ram)와 CPU에 저장됩니다.

메인 메모리 : 프로세스 전체 데이터(코드, 데이터, 힙, 스택)가 저장됩니다.

(PCB는 메인 메모리 안에 있지만, 운영체제(OS)가 관리하는 커널 영역에 존재합니다.)

PCB : 프로세스의 중요한 정보 (프로세스 상태, 레지스터 값, 스케줄링 정보 등)가 저장되며, 프로세스가 실행되지 않을 때에도 유지됩니다.

CPU 레지스터 : 프로세스가 실행 중일 때, 연산에 필요한 정보(PC, SP 등)가 저장 됩니다.

</div>
</details>

<details> 
<summary><b>문맥교환은 왜 필요한가요?</b></summary>
<div markdown="1">

CPU는 한 번에 하나의 프로세스만 실행할 수 있습니다. 하지만 운영체제는 여러 프로세스를 동시에 실행하는 것처럼 보이게 만들기 위해 빠르게 전환하면서 실행해야 합니다. 이때 문맥 교환을 통해 여러 프로세스를 번갈아 실행할 수 있으며, 이를 통해 멀티 태스킹 환경을 지원하고 CPU 자원을 효율적으로 활용할 수 있습니다.

</div>
</details>

---

## 박상윤

<details> 
<summary><b>PCB(프로세스 컨트롤 블록)안에 어떤 정보들이 있나요?</b></summary>
<div markdown="1">

- 프로세스 식별자(Process ID, PID) : 프로세스 식별 번호
- 프로세스 상태 : new, ready, running, waiting, terminated 등의 상태를 저장
- 프로그램 카운터 : 프로세스가 다음에 실행할 명령어의 주소
- CPU 레지스터 : CPU에서 사용한 레지스터의 값을 잃지 않기 위해 PCB에 그 값을 저장
- CPU 스케줄링 정보 : 프로세스의 우선순위, 스케줄 큐에 대한 포인터 등
- 메모리 관리 정보 : 페이지 테이블 또는 세그먼트 테이블 등과 같은 정보를 포함
- 입출력 상태 정보 : 프로세스에 할당된 입출력 장치들과 열린 파일 목록
- 어카운팅 정보 : 사용된 CPU 시간, 시간제한, 계정 번호 등

</div>
</details>

<details> 
<summary><b>프로세스 상태 정보를 통해 어떤 작업을 수행할 수 있나요?</b></summary>
<div markdown="1">

프로세스 상태 정보를 기반으로 **CPU 스케줄링**을 수행합니다.

프로세스의 상태 정보를 저장하고 복원하여 **다중 프로세스 환경에서 컨텍스트 스위칭**을 수행할 수 있습니다.

프로세스 상태 정보를 활용해 **동기화 기법(세마포어, 뮤텍스)**을 적용할 수 있습니다.

- 실행 중인 프로세스가 공유 자원에 접근하려 할 때 대기 상태로 변경하여 데이터 충돌 방지

</div>
</details>

<details> 
<summary><b>컨텍스트 스위칭이란 무엇인가요?</b></summary>
<div markdown="1">

운영체제가 현재 실행 중인 프로세스의 상태를 저장하고 ,다른 프로세스의 상태를 복원하여 실행을 전환하는 과정을 의미합니다.

</div>
</details>

<details> 
<summary><b>컨텍스트 스위칭은 어떤 상황에 발생하나요?</b></summary>
<div markdown="1">

**프로세스 스케줄링** : 멀티태스킹 환경에서 여러 프로세스를 실행하기 위해 운영체제는 CPU 스케줄러를 사용하여 프로세스를 교체합니다.

**인터럽트 발생시** : 입출력(I/O)요청, 타이머 인터럽트, 시스템 호출 등으로 실행 중이던 프로세스가 중지되고, 다른 프로세스가 실행됩니다.

</div>
</details>

<details> 
<summary><b>컨텍스트 스위칭은 프로세스만 가능하다. (O, X)</b></summary>
<div markdown="1">

x : 스레드도 가능합니다.

</div>
</details>

<details> 
<summary><b>스레드 컨텍스트 스위칭은 무엇이고, 프로세스 컨텍스트 스위칭보다 왜 빠를까요?</b></summary>
<div markdown="1">

같은 프로세스 안의 스레드끼리 컨텍스트 스위칭이 일어나는 것입니다.

스레드는 같은 **프로세스 내에서 코드, 데이터, 힙 영역을 공유**하기 때문에 **스택과 레지스터 정보만 변경**하면 됩니다. 즉, 프로세스 컨텍스트 스위칭보다 더 적은 오버헤드로 빠르게 수행이 가능합니다.

프로세스 **컨텍스트 스위칭**

**커널 모드 전환 + CPU register 상태 교체** + **가상 메모리 주소 처리(MMU 수정 + TLB 캐시 비우기)**

</div>
</details>

<details> 
<summary><b>프로세스 컨텍스트 스위칭 시에 새로운 프로세스의 실제 주소 체계를 바라보도록 수정하는 매개체는 무엇인가요?</b></summary>
<div markdown="1">

**MMU(Memory Management Unit)** : CPU와 물리 메모리(RAM) 사이에서 메모리 주소 변환 및 보호 기능을 수행하는 하드웨어 컴포넌트
**가상 주소 → 물리 주소 변환**
프로세스가 사용하는 가장 주소를 실제 물리 메모리 주소로 변환하여 CPU가 RAM에 접근할 수 있게 해줍니다.

</div>
</details>

<details> 
<summary><b>리눅스 커널에서 프로세스의 정보를 저장하는 구조체의 이름은 무엇일까요?</b></summary>
<div markdown="1">

task_struct
```c
struct task_struct { 
  pid_t pid; // 프로세스 ID 
  volatile long state; // 프로세스 상태 
  struct list_head tasks; // 프로세스 리스트 
  int prio; // 우선순위 
  struct mm_struct *mm; // 프로세스의 메모리 정보 
  struct files_struct *files; // 열린 파일 정보 
  struct thread_info *thread; // CPU 레지스터 및 스택 정보 
  struct task_struct *parent; // 부모 프로세스 정보 
  struct list_head children; // 자식 프로세스 리스트 
  struct list_head sibling; // 형제 프로세스 리스트 
 };
```

</div>
</details>

<details> 
<summary><b>리눅스 커널에서 활동중인 프로세스의 task_struct는 어떠한 자료구조를 사용해서 묶여 있나요?</b></summary>
<div markdown="1">

Double Linked List를 사용합니다.

</div>
</details>

---

## 변하영

<details> 
<summary><b>컨텍스트 스위칭은 언제 일어날까요?</b></summary>
<div markdown="1">

Interrupt 발생, 멀티태스킹시 프로세스간 전환, 커널모드와 사용자모드 전환 등의 이유로 발생합니다.

</div>
</details>

<details> 
<summary><b>컨텍스트 스위칭 시 커널 스택과 PCB는 각각 어떤 역할을 하나요?</b></summary>
<div markdown="1">

커널 스택은 현재 실행중인 프로세스의 실행 상태(레지스터, 함수 호출정보)를 저장하는 공간입니다. PCB는 커널 스택 포인터, 프로그램 카운터, 프로세스 상태, 스케줄링 정보 등을 저장하여 프로세스 관리에 사용됩니다.

</div>
</details>

<details> 
<summary><b>컨텍스트 스위칭 시 캐시 오염이란 무엇인가요?</b></summary>
<div markdown="1">

CPU 캐시는 실행중인 프로세스의 데이터를 저장합니다. 이때 컨텍스트 스위칭이 발생하면 새로운 프로세스가 이전 프로세스의 캐시 데이터를 사용할 수 없게 되어 캐시 미스가 증가합니다. 이를 캐시 오염이라고 합니다.

</div>
</details>

<details> 
<summary><b>프로세스 컨텍스트 스위칭 시 많은 비용이 소모되는 이유를 설명해주세요</b></summary>
<div markdown="1">

프로세스 컨텍스트 스위칭 시에는 커널 모드 전환과 CPU 레지스터 상태 저장 및 복원 작업이 수행되며, 추가적으로 새로운 주소 공간을 사용하는 경우 MMU(Memory Management Unit) 업데이트 및 TLB 플러시가 발생할 수 있습니다. 이러한 작업들은 메모리 접근 속도를 저하시켜 컨텍스트 스위칭 비용을 증가시킵니다.

</div>
</details>

<details> 
<summary><b>프로세스 컨텍스트 스위칭과 스레드 컨텍스트 스위칭의 차이점은 무엇인가요?</b></summary>
<div markdown="1">

프로세스 컨텍스트 스위칭은 주소 공간이 변경되므로, MMU 업데이트와 TLB 플러시가 필요하여 비용이 큽니다.
반면, 스레드 컨텍스트 스위칭은 같은 주소 공간을 공유하기 때문에 레지스터와 스택만 변경하면 되므로 비용이 낮습니다.
따라서 멀티스레딩이 멀티프로세스보다 컨텍스트 스위칭 비용이 적어 빠르게 동작할 수 있습니다.

</div>
</details>

<details> 
<summary><b>PCB는 어떻게 관리되나요?</b></summary>
<div markdown="1">

PCB는 커널 주소 공간의 Data 영역에 저장되며, 프로세스 테이블에서 관리됩니다. 프로세스 테이블은 여러 개의 PCB를 저장하는 운영체제의 자료구조로, LinkedList 방식으로 관리됩니다. 주소값으로 연결이 이루어져 있는 연결리스트이기에 삽입 삭제가 용이합니다.

</div>
</details>

