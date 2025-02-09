## 김수훈

<details>
<summary><strong>대표적인 CPU 스케줄링 알고리즘을 하나만 설명해주세요</strong></summary>
<div>

- **FCFS (First Come First Serve)**: 먼저 도착한 프로세스가 먼저 실행되는 알고리즘 입니다. 비선점형이며 먼저 도착한 프로세스의 작동 시간이 긴 경우 짧은 작업들이 오래 기다려야 하는 **호위 효과** 문제가 발생할 수 있습니다.
- **Round Robin (RR)**: 각 프로세스에 일정한 시간을 할당하여 순환 실행을 하는 알고리즘입니다. 하나의 프로세스가 끝날 때까지 기다리지 않기 때문에 선점형 스케줄링에 속합니다.

</div>
</details>

<details>
<summary><strong>라운드 로빈 스케줄링의 장점과 단점을 설명해주세요</strong></summary>
<div markdown="1">

- **장점**: 모든 프로세스가 일정한 시간 동안 실행되기 때문에 CPU 분배가 공정하게 이루어집니다.
- **단점**: 각 프로세스에게 할당되는 일정한 시간인 Time Quantum이 너무 작으면 컨텍스트 스위칭 비용이 증가할 수 있습니다.

</div>
</details>

<details>
<summary><strong>컨텍스트 스위칭이 뭔지 간단하게 설명해주세요</strong></summary>
<div markdown="1">

- CPU가 실행 중인 프로세스를 변경할 때, 현재 프로세스의 상태(Context)를 저장하고 새로운 프로세스의 상태를 로드하는 과정을 말합니다.

</div>
</details>

<details>
<summary><strong>선점형 비선점형 모두 우선순위 스케줄링이 있는데, 차이가 무엇인가요?</strong></summary>
<div markdown="1">

- 둘 다 프로세스의 우선순위 순서대로 처리한다는 점은 같지만, 비선점형과 다르게 선점형에서의 우선순위 스케줄링은 더 높은 우선순위의 프로세스가 도착하면 기존의 작업을 중단한다는 점에서 차이가 있습니다.

</div>
</details>

<details>
<summary><strong>기아 현상을 해결할 수 있는 방법에는 뭐가 있을까요?</strong></summary>
<div markdown="1">

- 시간이 지날수록 낮은 우선순위의 프로세스 우선순위를 점진적으로 높이는 에이징 기법을 사용하거나 라운드 로빈을 적용해서 모든 프로세스가 일정한 시간 동안 CPU를 사용할 수 있도록 보장하는 방법이 있습니다.

</div>
</details>

<details>
<summary><strong>현대 운영체제, 예를 들면 mac이나 window에서 cpu 스케줄링은 어떻게 이루어지고 있는지 아시나요?</strong></summary>
<div>

- 운영체제마다 CPU 스케줄링 방식이 다르지만, 공통적으로 멀티태스킹 환경을 최적화하기 위해 선점형 스케줄링을 사용하는 것으로 알고 있습니다.
- 예를 들어, Windows는 우선순위 기반 스케줄링을 적용하여 중요한 프로세스를 빠르게 실행합니다. macOS는 Hybrid Scheduling을 사용하며, 모바일 OS에서는 배터리 효율성을 고려한 스케줄링 기법이 적용됩니다.

</div>
</details>


<details>
<summary><strong><꼬리 질문> 우선순위 기반 스케줄링과 Hybrid Scheduling을 간단하게 설명 해주세요</strong></summary>
<div>

- 우선순위 기반 스케줄링은 각 프로세스에 우선순위(Priority)를 부여하고, 높은 우선순위를 가진 프로세스를 먼저 실행하는 방식이며 
- hybrid scheduling은 하나의 스케줄링 알고리즘만 사용하지 않고, 여러 개의 스케줄링 방식을 조합하여 적용하는 기법입니다.

</div>
</details>

---

## 박상윤

<details>
<summary><strong>프로세스를 기준으로 크롬 웹에서 구글을 켜고 검색어를 입력하는 순간 어떤일이 발생하나요?</strong></summary>
<div>

- 검색어를 입력하는 순간, 키보드 입력(입출력, I/O) 이벤트가 발생하면서 입력 장치가 인터럽트(Interrupt)를 발생시켜 현재 실행 중인 프로세스를 대기(Waiting) 상태로 전환합니다.

</div>
</details>

<details>
<summary><strong>서버의 메모리가 가득 차서 과부하가 걸렸다면, 운영체제는 어떤 방식으로 이를 해결할까요? </strong></summary>
<div>

- 운영체제는 중기 스케줄러를 사용하여 메모리 공간을 확보하기 위해 스왑 아웃(Swap Out) 을 수행할 수 있습니다.

</div>
</details>
  
<details>
<summary><strong>대규모 시스템에서 다중 사용자 요청을 효율적으로 처리하기 위한 스케줄링 기법은 무엇이 있나요?</strong></summary>
<div>

- 멀티 레벨 큐 스케줄링(Multi-Level Queue Scheduling) 이 효과적인 방법 중 하나입니다.

- 대규모 시스템에서는 **다양한 우선순위를 가진 프로세스들이 공존**하며, 동일한 방식으로 처리하면 **응답 속도가 중요한 작업이 지연** 될 수 있습니다. 멀티 레벨 큐 스케줄링은 **프로세스를 성격에 따라 여러 개의 큐로 분리하여 최적화된 방식으로 실행** 할 수 있습니다.

</div>
</details>
  
<details>
<summary><strong>서버에서 특정 프로세스가 장시간 실행되면서 CPU를 독점하고 있습니다. 이를 해결할 수 있는 스케줄링 방법은 무엇인가요?</strong></summary>
<div>

- 운영체제에서는 비선점형 스케줄링과 선점형 스케줄링이 존재하는데, CPU를 독점하는 문제는 선점형 스케줄링을 활용하여 해결할 수 있습니다.

</div>
</details>
  
<details>
<summary><strong>실시간 서비스(예: 게임 서버)에서 라운드 로빈(Round Robin) 스케줄링을 적용하면 발생할 수 있는 문제는 무엇인가요?</strong></summary>
<div>

- 라운드 로빈 스케줄링은 모든 프로세스에 동일한 CPU 시간을 할당하는 방식으로, 실시간 성능이 중요한 서비스에서는 오버헤드가 발생해 응답 속도가 느려질 수 있습니다.
- **콘텍스트 스위칭(Context Switching) 비용 증가**
- **응답 시간이 중요한 프로세스의 지연**

</div>
</details>
  
<details>
<summary><strong>특정 프로세스가 CPU를 거의 할당받지 못해 오랫동안 실행되지 않는 문제가 발생했습니다. 현재 CPU는 어떤 스케줄링 기법을 사용하나요?</strong></summary>
<div>

- 운영체제에서 기아 상태(Starvation)는 SJF(Shortest Job First)나 SRTF(Shortest Remaining Time First) 같은 알고리즘을 사용할 때 낮은 우선순위를 가진 프로세스가 CPU를 할당받지 못하는 문제입니다.

</div>
</details>

---
  
## 변하영

<details>
<summary><strong>컨텍스트 스위칭이 무엇인지 설명해보세요</strong></summary>
<div>

- 컨텍스트 스위칭(Context Switching)은 CPU가 현재 실행 중인 프로세스(또는 스레드)의 상태(Context)를 저장하고, 다른 프로세스(또는 스레드)로 전환하는 과정을 의미합니다. 여기서 컨텍스트란 프로세스의 레지스터 정보(CPU 상태), 프로그램 카운터, 스택, 메모리 정보 등을 포함합니다.

</div>
</details>
  
<details>
<summary><strong>동시성과 병렬성을 비교해 설명해보세요</strong></summary>
<div>

- 동시성은 하나의 코어에서 여러 스레드가 번갈아가며 실행하는 것을 말합니다. 즉, 동시에 실행하는 것이 아닌, CPU가 작업마다 시간을 분할해 적절한 컨텍스트 스위칭을 통해 동시에 실행되는 것처럼 보이게 하는 것입니다.
- 반면에, 병렬성은 멀티 코어에서 여러 스레드를 동시에 실행하는 것을 말합니다. 동일성과 달리 여러 작업을 다른 코어, 프로세스, 별도 컴퓨터 등에서 동시 실행 가능합니다.

</div>
</details>
  
<details>
<summary><strong>프로세스 스케줄링이란 무엇이며, 왜 필요한가요?</strong></summary>
<div>

- 프로세스 스케줄링은 Ready Queue에 대기 중인 프로세스 중 어떤 프로세스에게 CPU를 할당할 것인지 결정하는 작업을 의미합니다.
스케줄링의 주된 목적은 멀티 프로세스 환경에서 모든 프로세스를 공평하게 실행하는 것입니다.
- 또한 세부적인 목적으로는 자원을 효율적으로 사용하는 것, 높은 우선순위의 프로세스부터 먼저 실행하는 것, 사용자에게 일정 시간 내에 응답하는 것, 마지막으로 특정 프로세스가 무한히 연기되지 않도록 하는 것이 있습니다.

</div>
</details>
  
<details>
<summary><strong>스케줄링 평가기준에 대해 설명해주세요</strong></summary>
<div>

- 크게 시스템 입장의 성능 척도와 프로그램 입장의 성능 척도로 나눌 수 있습니다.
- 시스템 입장의 성능 척도로는 CPU 이용률, 처리율이 있고, 프로그램 입장의 성능 척도로는 반환시간, 대기 시간, 반응 시간, 실행 시간이 있습니다. 시스템 입장의 성능 척도는 늘리고, 프로그램 입장의 성능척도는 줄이는 것이 좋습니다.

</div>
</details>
  
<details>
<summary><strong>프로세스 스케줄링의 유형에는 무엇이 있으며, 각각의 특징은 무엇인가요?</strong></summary>
<div>

- 프로세스 스케줄링은 크게 비선점형(Non-preemptive)과 선점형(Preemptive)으로 나뉩니다.
- 비선점형 스케줄링은 한 번 CPU를 할당받으면 종료될 때까지 계속 실행됩니다. First Come Fistst Served, Shortest Job First, Highest Response Ratio Next 등이 있습니다.
- 선점형 스케줄링은 실행 중인 프로세스더라도 더 높은 우선순위의 프로세스가 오면 CPU를 양보합니다. Round Robin, Shortest Remaining Time First, Multi-level Queue 등이 있습니다. 운영체제는 이 알고리즘을 상황에 맞게 조합하여 사용합니다.

</div>
</details>
  
<details>
<summary><strong>FCFS (First-Come, First-Served) 스케줄링의 장점과 단점은 무엇인가요?</strong></summary>
<div>

- FCFS (First-Come, First-Served)는 먼저 도착한 프로세스를 먼저 실행하는 방식입니다.
- 장점으로는 구현이 간단하며 공정하고, 선점이 없어 컨텍스트 스위칭 비용이 없다는 점입니다.
- 단점으로는 실행시간이 긴 프로세스가 먼저 오면 이후 프로세스들의 대기 시간이 길어지는 convoy effect가 발생할 수 있다는 점입니다.

</div>
</details>
  
<details>
<summary><strong>SJF (Shortest Job First)와 SRTF (Shortest Remaining Time First)의 차이는 무엇인가요?</strong></summary>
<div>

- SJF와 SRTF는 실행 시간이 짧은 프로세스를 우선 실행하는 알고리즘이지만, 선점 여부에서 차이가 있습니다. SJF는 비선점형 방식이고, SRTF는 선점형 방식입니다. 따라서 SRTF는 실행중이더라도 더 짧은 실행 시간이 남은 프로세스가 들어오면 해당 프로세스가 CPU를 차지하게 됩니다. 이는 실행 시간이 짧은 작업이 빠르게 완료되지만, 컨텍스트 스위칭이 자주 발생하여 오버헤드가 증가할 수 있습니다.

</div>
</details>
  
<details>
<summary><strong>Round Robin 스케줄링이란 무엇이며, 장점과 단점은 무엇인가요?</strong></summary>
<div>

- Round Robin (RR) 스케줄링은 프로세스마다 일정한 시간(Time Quantum)만큼 CPU를 할당한 후, 다음 프로세스로 교체하는 방식입니다.
- 장점으로는 모든 프로세스에 공평하여 응답 시간이 일정하다는 점입니다. 하지만 단점으로는 Time Quantum이 너무 크면 FCFS와 비슷해지고, 너무 작으면 컨텍스트 스위칭이 너무 자주 발생해 오버헤드가 증가한다는 점입니다. 따라서 적절한 Time Quantum을 설정하는 것이 중요합니다.

</div>
</details>
  
<details>
<summary><strong>다단계 큐(Multi-Level Queue) 스케줄링과 다단계 피드백 큐(Multi-Level Feedback Queue) 스케줄링의 차이는 무엇인가요?</strong></summary>
<div>

- 다단계 큐(MLQ)와 다단계 피드백 큐(MLFQ)는 프로세스를 여러 개의 큐로 나누어 스케줄링하는 방식입니다.
- Multi-Level Queue의 경우 프로세스를 우선 순위별로 여러 개의 고정된 큐에 할당하고, 각 큐는 다른 스케줄링 방식을 적용할 수 있습니다.
- 반면에 Multi-Level Feedback Queue는 Multi-Level Queue에서 큐 간 이동이 가능하도록 개선된 방식입니다. 처음에는 높은 우선순위 큐에서 시작하지만, CPU를 오래 사용하면 낮은 우선순위 큐로 이동시킵니다. 짧은 작업은 빠르게 끝내고, 긴 작업은 차츰 낮은 우선순위로 배치하여 균형을 맞춥니다. 이외에도 다른 변형을 적용할 수 있습니다.

</div>
</details>
  
<details>
<summary><strong>프로세스 스케줄링에서 기아 현상(Starvation)이란 무엇이며, 해결 방법은 무엇인가요?</strong></summary>
<div>

- 기아 현상(Starvation)은 우선순위가 낮은 프로세스가 계속 실행되지 못하고 대기하는 문제를 말합니다.SJF, SRTF 같은 스케줄링 알고리즘에서 발생할 수 있습니다.
- 이를 해결하기 위해서는 대기 시간이 길어질수록 우선순위를 높이는 방식인 Aging기법을 사용할 수 있습니다.
- 또는 시간이 지나면 낮은 우선순위 프로세스도 점진적으로 실행 가능하도록 하는 MLFQ를 사용할 수 있습니다.

</div>
</details>
  
<details>
<summary><strong>스케줄링의 단계에 대해 설명하세요</strong></summary>
<div>

- 장기 스케줄링은 준비 큐에 어떤 프로세스를 넣을 결정하여 메모리에 올라가는 프로세스 수를 조정합니다. 현대 운영체제에서는 시분할 시스템을 사용하기 때문에 대부분 사용하지 않습니다.
- 이때, 시분할 시스템은 각 프로세스에 CPU에 대한 일정시간을 할당하여 주어진 시간동안 프로그램을 수행할 수 있게하는 시스템입니다.
- 중기 스케줄링은 메모리에 로드된 프로세스 수를 동적으로 조절합니다.
- 단기 스케줄링은 레디 큐에 있는 대기 상태 프로세스 중 어떤 프로세스를 실행할지 결정합니다. CPU 스케줄링이라고도 합니다.

</div>
</details>

---
  
## 신예지

<details>
<summary><strong>CPU 스케줄링의 목적에 대해 설명해주세요</strong></summary>
<div>

- CPU 스케줄링의 주된 목적은 멀티 프로세스 환경에서 모든 프로세스를 공평하게 실행하는 것으로 세부적으로는 공평성, 효율성, 안정성, 반응 시간 보장, 무한 연기 방지의 목적이 있습니다.
- 모든 프로세스는 공평하게 실행돼야 하고, 자원을 효율적으로 사용하여 사용되지 않는 시간이 없도록 해야 합니다. 또 우선순위를 고려하여 높은 우선순위의 프로세스를 먼저 처리하도록 해야 하고, 프로세스는 일정 시간 내에 응답할 수 있어야 합니다. 마지막으로 특정 프로세스에 대한 처리가 무한히 연기되지 않도록 해야 한다.

</div>
</details>

<details>
<summary><strong>장기, 중기, 단기 스케줄링에 대해 각각 간략하게 설명해주세요</strong></summary>
<div>

- 장기 스케줄링은 프로세스가 생성된 상태에서 준비 상태로 이동할 때 사용됩니다. 중기 스케줄링은 swapping 할 때 사용되는데, 어떤 프로세스를 swap out 할 지, 어떤 프로세스를 메인 메모리에 swap in 할 지 결정합니다. 단기 스케줄링은 Ready Queue에 들어있는 프로세스를 언제 실행할 지 결정합니다. 어떤 프로세스를 실행할 지에 따라 프로세스의 실행시간과 대기시간이 달라지므로 시스템 성능에 직접적인 영향을 끼칩니다.

</div>
</details>
 
<details>
<summary><strong>스와핑에 대해 설명해주세요</strong></summary>
<div>

- 스와핑은 컴퓨터의 메모리 공간보다 실제 프로세스의 크기가 크기 때문에 일부 프로세스를 저장공간에 옮겨 저장하고, 필요할 때 다시 메모리에 로드하는 것을 말합니다. 스와핑을 하면 컴퓨터의 메모리 공간보다 많은 프로세스를 실행할 수 있다는 장점이 있습니다.

</div>
</details>
  
<details>
<summary><strong>CPU 스케줄링을 평가하는 척도를 설명해주세요</strong></summary>
<div>

- cpu 스케줄링을 평가할 때 프로세스에 요청이 발생했을 때 응답까지 걸리는 시간인 응답시간(response time), 프로세스가 로드된 이후부터 종료될 때까지 걸리는 시간인 반환시간(turnaround time), 전체 시간 중 CPU가 놀지 않고 일한 시간의 비율인 CPU 사용률(CPU Utilization), 단위 시간 당 실행한 프로세스의 수(throughput) 네 가지 척도가 사용됩니다.

</div>
</details>
  
<details>
<summary><strong>비선점형 스케줄링의 의미와 대표적인 비선점형 스케줄링에 대해 설명해주세요</strong></summary>
<div>

- 비선점형 스케줄링은 한 프로세스가 CPU를 할당받으면 작업 종료 후 CPU를 반환할 때까지 다른 프로세스가 CPU를 점유할 수 없는 방식을 말합니다. 대표적인 비선점형 스케줄링으로는 FCFS(First Come First Served), SJF(Shortest Job First), Priority, HRRN(Highest Resoponse Ratio Next) 이 있습니다.

</div>
</details>
  
<details>
<summary><strong>선점형 스케줄링의 의미와 대표적인 선점형 스케줄링에 대해 설명해주세요</strong></summary>
<div>

- 선점형 스케줄링은 우선순위에 따라 현재 CPU를 점유중인 프로세스를 강제로 중단시키고 다른 프로세스에게 CPU를 할당하는 방식을 말합니다. 대표적인 선점형 스케줄링으로는 RR(Round Robin), SRTF(Shortest Remaining Time First), 다단계 큐(Multi Level Queue) 가 있습니다.

</div>
</details>
  
<details>
<summary><strong>SJF 스케줄링에 대해 설명해주세요</strong></summary>
<div>

- SJF 스케줄링은 실행 시간이 짧은 프로세스의 우선순위가 높은 스케줄링 방식으로 비선점형 알고리즘 중 하나입니다. 평균 대기 시간이 짧은 장점이 있지만 실행 시간이 긴 프로세스의 경우 영원히 CPU를 할당받지 못하는 starvation이 발생할 수 있고, CPU burst time(CPU 실행 시간)을 정확히 알 수 없어 예측 시간보다 더 길게 CPU를 점유할 수 있다는 단점이 있습니다.

</div>
</details>
  
<details>
<summary><strong>HRRN 스케줄링에 대해 설명해주세요</strong></summary>
<div>

- HRRN 스케줄링은 Response Ratio를 계산하여 해당 값이 가장 높은 프로세스를 우선적으로 스케줄링하는 방식으로 비선점형 알고리즘 중 하나입니다. ratio를 계산하여 실행 시간과 대기 시간을 고려하는 방식이고, starvation 발생 가능성이 없습니다.

</div>
</details>
  
<details>
<summary><strong>RR 스케줄링에 대해 설명해주세요</strong></summary>
<div>

- RR 스케줄링은 모든 프로세스를 순서대로 time quantum 동안 실행하며, time quantum을 초과하면 time out을 하여 현재 실행 중인 프로세스를 중단시키는 방식으로 선점형 알고리즘 중 하나입니다.

</div>
</details>
  
<details>
<summary><strong>SRTF 스케줄링에 대해 설명해주세요</strong></summary>
<div>

- SRTF 스케줄링은 남은 실행시간이 짧은 프로세스가 우선순위를 갖는 방식으로 선점형 알고리즘 중 하나입니다. 평균 대기시간이 짧다는 장점이 있지만, starvation이 발생할 수 있고 CPU burst time을 예측할 수 없다는 단점이 있습니다.

</div>
</details>

---
  
## 이소원

<details>
<summary><strong>cpu스케줄링이란?</strong></summary>
<div>

- 다중 프로세스 또는 다중 스레드 환경에서 cpu 자원을 효율적으로 할당하는 방법을 결정하는 작업을 말한다.
- 여러 프로세스 또는 스레드가 실행을 기다리는 상황에서 cpu를 어떤 순서로 얼마나 오랫동안 할당할지 관리하는 중요한 운영체제의 기능 중 하나이다.

</div>
</details>

<details>
<summary><strong>cpu 스케줄링의 목적은?</strong></summary>
<div>

- 공평성 : 모든 프로세스가 공평하게 배정받고,
- 안정성 : 시스템이 실행되는 중 강제로 다른 시스템이 점유하거나 파괴하려는 프로세스로부터 지원을 보호하기 위해
- 효율성
- 반응시간 보장

</div>
</details>
  
<details>
<summary><strong>선점형과 비선점형의 차이는?</strong></summary>
<div>

- 선점형은 각 스케줄링에 따른 우선순위가 높은 프로세스가 실행되고 있는 프로세스를 중단시키고 우선순위가 높은 프로세스를 실행시키는 것을 선점형이라고 하고,
- 비선점형은 한 프로세스가 실행되면 끝날 때 까지 중단할 수 없는 것이다.

</div>
</details>
  
<details>
<summary><strong>라운드 로빈에 대해 설명</strong></summary>
<div>

- 선점형 스케줄링 알고리즘으로, 준비 큐에 도착한 순서에 따라 cpu 제어권을 받지만, 정해진 time slice에 따라 실행을 제한하는 스케줄링 알고리즘이다.
- cpu를 독점하지 않고 공평하게 이용할 수 있으며, 대화형 운영체제에 유용하다.

</div>
</details>
  
<details>
<summary><strong>rr 에서 타임 슬라이스를 너무 크게하거나 작게하면 어떤 문제가 발생할까?</strong></summary>
<div>

- 너무 작으면 **문맥 전환(Context Switching)이 자주 발생**하여 오버헤드 증가한다.
- 너무 크면 응답 시간이 길어진다.
- 적절한 타임 슬라이스 선택이 중요하다.

</div>
</details>
  
<details>
<summary><strong>convoy effect 설명</strong></summary>
<div>

- 프로세스 실행 시간에 따른 우선순위가 주어지는 스케줄링에서 짧은 스케줄링들이 먼저 실행되면서 길이가 긴 스케줄링이 뒤로 밀려 실행되지 못하는 것을 의미한다.
- 긴 작업이 먼저 실행되면 짧은 작업이 대기하는 현상이다.

</div>
</details>
  
<details>
<summary><strong>현재 운영체제에서 사용하는 스케줄링 기법과 간단한 설명</strong></summary>
<div>

- 현대 운영체제(Linux, Windows)는 **다단계 피드백 큐(Multi-level Feedback Queue) 기반 스케줄링**을 사용.
- 따라서 다양한 우선순위 프로세스를 처리하고 응답 속도와 처리량을 균형 있게 유지할 수 있다.

</div>
</details>
  
<details>
<summary><strong>기아상태를 해결할 수 있는 방법은?</strong></summary>
<div>

- 프로세스가 원하는 자원을 계속 할당 받지 못하는 상태를 말한다.
- 이를 해결하기 위해 공평한 자원 할당을 위해 시간 제한을 두거나 우선순위를 둘 수 있다.
- sjf와 같은 스케줄링에서 발생하며 이를 해결하기 위해 라운드 로빈이나 우선순위 스케줄링이 있다.

</div>
</details>
  
<details>
<summary><strong>멀티 레벨 큐 스케줄링에 대해 설명해주세요.</strong></summary>
<div>

- 레디큐를 여러개로 나누어 관리하는 스케줄링으로, 우선순위가 높은 큐를 모두 처리한 후, 낮은 우선순위의 큐를 처리하는 방식.
    - 일반적으로 CPU 실행시간이 짧은 대화형 프로세스를 담기 위한 전위 큐와(라운드 로빈 방식 적용)
    - CPU 실행시간이 긴 계산위주의 프로세스를 담기 위한 후위 큐로 분할되어 운영됩니다.(FCFS 방식 적용)

</div>
</details>
  
<details>
<summary><strong>멀티 레벨 피드백 큐 스케줄링에 대해 설명해주세요.</strong></summary>
<div>

- 멀티 레벨 큐 스케줄링 방식에서 프로세스들이 우선 순위를 가진 큐들을 다른 큐로 이동할 수 있는 방식
	- 현재 큐에서 실행을 끝내지 못하면 하위 우선순위 큐로 이동하게 됩니다.
	- 우선순위가 낮은 레디큐에서 너무 오래 기다린 프로세스에 대해서는 다시 우선 순위가 높은 레디큐로 보내는 에이징 기법을 적용 합니다.

</div>
</details>
  
<details>
<summary><strong>라운드로빈을 실제로 적용하기 어려운 이유는?</strong></summary>
<div>

- 실제 동작환경에서는 프로세스의 실행 시간을 예측하기 어렵다.
- 라운드 로빈에서의 적절한 타임 슬라이스를 지정하는 것이 어렵다.

</div>
</details>

