## 신예지

<details>
<summary><b>페이지 교체 알고리즘은 왜 필요할까요?</b></summary>
<div markdown="1">

페이지 부재율을 최소화 하여 성능을 높이기 위해 필요합니다.

</div>
</details>

<details>
<summary><b>Belady's Anomaly에 대해 설명해주세요</b></summary>
<div markdown="1">

프레임의 개수가 많아져도 page fault가 줄어들지 않고 늘어나는 현상을 말합니다.

</div>
</details>

<details>
<summary><b>Belady's Anomaly는 어떤 페이지 교체 알고리즘에서 발생할까요?</b></summary>
<div markdown="1">

FIFO

</div>
</details>

<details>
<summary><b>참조비트를 사용하는 페이지 교체 알고리즘을 모두 말해주세요</b></summary>
<div markdown="1">

NRU, Clock, LRU(에 근사하는 알고리즘 - SCR)

</div>
</details>

<details>
<summary><b>LRU 구현 방식에서 카운터로 구현하는 것과 스택으로 구현하는 것의 공통점을 말해주세요</b></summary>
<div markdown="1">

오버헤드가 발생한다.

</div>
</details>

<details>
<summary><b>LRU 근사 알고리즘 중 부가적 참조 비트 알고리즘에서 가장 오랫동안 참조되지 않은 페이지 일수록 참조 비트의 정수값이 클까요 작을까요?</b></summary>
<div markdown="1">

작습니다.

</div>
</details>

<details>
<summary><b>2차 기회 알고리즘(Second Chance Replacement)에 대해 설명해주세요</b></summary>
<div markdown="1">

페이지가 선택될 때마다 참조 비트를 확인하여 참조 비트가 0이면 바로 교체하고, 1이면 한 번 더 기회를 주고 다음 페이지를 선택하는 알고리즘입니다.

</div>
</details>

<details>
<summary><b>LFU 알고리즘에서 만약 교체 대상인 페이지가 여러 개일 경우 어떻게 교체하나요?</b></summary>
<div markdown="1">

LRU 알고리즘에 따라 교체합니다.

</div>
</details>

---

## 변하영

<details>
<summary><b>FIFO 알고리즘이 성능이 좋지 않은 이유는 무엇일까요?</b></summary>
<div markdown="1">

FIFO는 단순히 먼저 들어온 페이지를 먼저 내보내는 방식입니다.  
특정 상황에서는 자주 사용되는 페이지가 먼저 제거될 수도 있고, 특히 Belady’s Anomaly가 발생하면 프레임 수를 늘려도 성능이 오히려 나빠집니다.

</div>
</details>

<details>
<summary><b>LRU의 성능이 좋은 이유는 무엇일까요?</b></summary>
<div markdown="1">

LRU는 가장 오랫동안 사용되지 않은 페이지를 교체하는 방식으로, 시간 지역성 원리를 잘 반영합니다.  
즉 최근에 사용된 페이지는 앞으로도 다시 사용될 확률이 높기 때문에 메모리에 유지하고, 그렇지 않은 페이지를 교체합니다.

</div>
</details>

<details>
<summary><b>LRU의 단점은 무엇일까요?</b></summary>
<div markdown="1">

구현이 어렵고 높은 오버헤드를 가집니다.  
LRU 구현을 위해서는 각 페이지의 사용 시간을 기록해야 하는데 이를 위해 카운터나 스택을 관리해야 합니다.

</div>
</details>

<details>
<summary><b>OPT 방식은 왜 사용되지 않나요?</b></summary>
<div markdown="1">

OPT 방식은 앞으로 오랫동안 사용되지 않을 페이지를 교체하는 방식입니다.  
하지만 현실에서는 미래의 메모리 접근 패턴을 알 수 없기 때문에 구현할 수 없습니다.

</div>
</details>

<details>
<summary><b>Clock 알고리즘과 LRU의 차이는 무엇인가요?</b></summary>
<div markdown="1">

Clock은 LRU를 근사하는 방식이지만, LRU처럼 정확하게 가장 오랫동안 사용되지 않은 페이지라고 보장할 수 없습니다.  
대신 원형 큐를 활용해 참조 비트가 0인 페이지를 교체하는 방식으로 동작합니다.

</div>
</details>

<details>
<summary><b>Clock 알고리즘 구현하는 방법에 대해 설명해주세요</b></summary>
<div markdown="1">

대상 페이지를 가리키는 포인터를 사용하는데, 포인터가 큐의 맨 아래로 내려가면 시계처럼 다시 큐의 처음을 가리키게 됩니다.  
참조 비트가 0인 것을 찾을 때까지 포인터를 이동시키고, 참조 비트가 1인 경우에는 0으로 바꾼 후 건너뜁니다.  
참조 비트가 0인 것을 찾으면 해당 페이지를 교체합니다.

</div>
</details>

---

## 박상윤

<details>
<summary><b>페이지 교체 알고리즘의 주요 목표는 무엇인가요?</b></summary>
<div markdown="1">

페이지 교체 알고리즘의 주된 목표는 **메모리 내에서 필요한 페이지가 없을 경우 발생하는 페이지 부재(page fault) 횟수를 최소화하여, 전체 시스템의 성능을 향상**시키는 것입니다.

</div>
</details>

<details>
<summary><b>OPT 알고리즘의 개념과 구현이 어려운 이유는 무엇일까요?</b></summary>
<div markdown="1">

OPT 알고리즘은 **앞으로 가장 오랫동안 사용되지 않을 페이지를 선택하여 교체하는 이론상 가장 효율적인 방법**입니다.  
그러나 이 알고리즘은 미래의 페이지 참조 패턴을 미리 알아야 하기 때문에 실제 운영체제에서는 구현이 불가능합니다.

</div>
</details>

<details>
<summary><b>FIFO(First In First Out) 알고리즘의 구조와 단점은 무엇인가요?</b></summary>
<div markdown="1">

FIFO 알고리즘은 **가장 먼저 메모리에 들어온 페이지를 교체 대상으로 선택**합니다.  
**큐(queue) 자료구조를 사용**하여, 새로 들어오는 페이지는 **큐의 맨 뒤**에 추가되고, **가장 오래된 페이지는 맨 앞에서 교체**됩니다.  
단점으로는 **단순히 순서를 기준으로 교체하기 때문에, 최근에 많이 참조된 페이지도 무작정 교체될 수 있고**, 프레임 수가 늘어날 때 오히려 페이지 부재 횟수가 증가하는 **Belady's Anomaly** 현상이 발생할 수 있습니다.

</div>
</details>

<details>
<summary><b>LRU(Least Recently Used) 알고리즘은 어떻게 구현되며, 구현 시 발생하는 오버헤드는 무엇인가요?</b></summary>
<div markdown="1">

**LRU 알고리즘은 가장 최근에 사용되지 않은 페이지를 교체 대상으로 선택**합니다.  
구현 방법에는 크게 두 가지가 있습니다:

- **카운터 방식**: 각 페이지에 사용 시간을 기록하여, 가장 오래전에 참조된 페이지를 찾아 교체합니다.  
- **스택 방식**: 참조된 순서를 스택에 저장하고, 페이지가 참조되면 해당 항목을 스택 상단으로 옮깁니다.

두 방식 모두 페이지 접근 시마다 **시간 정보를 갱신하거나 스택의 재배치가 필요**하여, 이에 따른 **추가적인 연산 비용(오버헤드)이 발생**합니다.

</div>
</details>

<details>
<summary><b>SCR(Second-Chance Replacement)와 Clock 알고리즘은 FIFO의 단점을 어떻게 보완하나요?</b></summary>
<div markdown="1">

SCR과 Clock 알고리즘은 FIFO 방식의 단점인  
**“단순히 오래된 순서대로 교체”되는 문제를 개선하기 위해 도입**되었습니다.

- **SCR(2차 기회 알고리즘)**: 각 페이지에 참조 비트를 추가하여, 페이지가 참조된 경우 한 번 더 기회를 주고, 참조 비트를 0으로 초기화한 후 다시 큐 뒤로 보냅니다.

- **Clock 알고리즘**: 원형 큐(시계 구조)를 사용하여, 참조 비트가 0인 페이지를 찾아 교체합니다.

두 방법 모두 최근에 사용된 페이지를 보호하여, 불필요한 교체를 줄이고 전체적인 성능 향상에 기여합니다.

</div>
</details>

<details>
<summary><b>🦫 Belady’s anomaly에서 Belady는 무엇을 의미할까요?</b></summary>
<div markdown="1">

Belady는 헝가리 출신의 컴퓨터 과학자인 **László Bélády**의 이름에서 유래되었습니다.  
그가 발견한 **Belady's Anomaly**는 페이지 프레임 수가 증가했음에도 불구하고 페이지 부재가 오히려 증가하는 역설적인 현상을 의미합니다.

</div>
</details>

---

## 이소원

<details>
<summary><b>FIFO는 어떻게 구현할 수 있나요?</b></summary>
<div markdown="1">

Queue

</div>
</details>

<details>
<summary><b>Belady의 이상현상 (Belady's Anomaly) 이란?</b></summary>
<div markdown="1">

프레임 개수가 많아져도 page fault가 줄어들지 않고, 오히려 늘어나는 현상입니다.

</div>
</details>

<details>
<summary><b>NUR보다 LRU를 더 많이 사용하는 이유를 설명해주세요</b></summary>
<div markdown="1">

NUR은 랜덤성과 오버헤드가 더 크기 때문입니다.  
LRU는 시간 지역성을 더 보장하고, 최근 사용된 페이지를 유지하기 때문에 더 정확합니다.

</div>
</details>

<details>
<summary><b>LRU와 Clock의 차이점을 설명해주세요</b></summary>
<div markdown="1">

- **LRU**: 가장 오랫동안 사용되지 않은 페이지를 찾는 데 효과적입니다.  
- **Clock**: 최근에 참조된 페이지를 보존하는 데 효과적입니다.

</div>
</details>

<details>
<summary><b>캐시 메모리에서 LRU가 많이 사용되는 이유는 무엇인가요?</b></summary>
<div markdown="1">

LRU(Least Recently Used)는 **시간 지역성**을 반영하기 때문에, 캐시에서 오랫동안 사용되지 않은 데이터를 제거하는 데 효과적입니다.

</div>
</details>

---

## 김수훈

<details>
<summary><b>페이지 교체 알고리즘은 언제 사용하는지를 주기억장치 혹은 물리 메모리와 연결 지어서 설명해주세요</b></summary>
<div markdown="1">

메모리를 관리하는 운영체제에서 필요한 페이지가 주기억장치에 적재되지 않았을 때(페이징 부재 시) 어떤 페이지 프레임을 선택해 교체할 것인지 결정할 때 사용합니다.

</div>
</details>

<details>
<summary><b>페이지 부재가 무엇인가요?</b></summary>
<div markdown="1">

프로세스 동작 중, 필요한 페이지가 물리 메모리에 없는 상황을 이야기합니다.

</div>
</details>

<details>
<summary><b>OPT(Optimal Replacement) 알고리즘의 개념과 실제 구현이 어려운 이유를 설명해보세요.</b></summary>
<div markdown="1">

OPT 알고리즘은 앞으로 가장 오랫동안 사용되지 않을 페이지를 교체하는 방법입니다.  
이론적으로 가장 효율적인 알고리즘이지만, 실제 구현이 어려운 이유는 미래의 페이지 참조 패턴을 정확히 예측해야 하기 때문입니다.  
운영체제는 프로그램이 앞으로 어떤 페이지를 언제 사용할지 미리 알 수 없어서, 이 알고리즘은 주로 다른 알고리즘의 성능을 평가하기 위한 **이론적 기준**으로 사용됩니다.

</div>
</details>

<details>
<summary><b>LRU 알고리즘의 단점을 설명하고, 극복하기 위한 근사 알고리즘들에는 무엇이 있나요?</b></summary>
<div markdown="1">

### 단점
- 프로세스가 주기억장치에 접근할 때마다 참조된 페이지 시간을 기록해야 하기 때문에 막대한 오버헤드가 발생함  
- 카운터나 스택, 큐와 같은 **별도의 하드웨어 지원**이 반드시 필요함  

**LRU 근사 알고리즘**으로는 참조 비트 알고리즘, 부가적 참조 비트 알고리즘, 2차 기회 알고리즘(SCR)이 있습니다.

</div>
</details>

<details>
<summary><b>LRU와 LFU 알고리즘이 가지는 공통적인 단점이 무엇인가요?</b></summary>
<div markdown="1">

LRU와 LFU의 공통적인 단점은 **구현을 위한 추가 공간과 시간 오버헤드**가 크다는 것입니다.  
LRU는 참조 시간을, LFU는 참조 횟수를 추적해야 하므로 **하드웨어 지원**이 필요합니다.

</div>
</details>

<details>
<summary><b>Clock 알고리즘의 작동 원리를 간단히 설명하고, 이 알고리즘이 LRU와 어떻게 근사하는지 설명해보세요.</b></summary>
<div markdown="1">

Clock 알고리즘은 SCR을 **원형 큐**로 구현한 것으로, 포인터가 시계 바늘처럼 회전하며 참조 비트가 0인 페이지를 찾습니다.  
참조 비트가 1인 페이지는 0으로 바꾸고 지나가며, 한 바퀴 도는 동안 참조되지 않은 페이지를 교체합니다.  

이는 LRU와 유사하게 **최근에 사용된 페이지를 보존**하지만, **정확한 참조 시간 순서를 추적하지는 않습니다.**

</div>
</details>

<details>
<summary><b>다음 토글 안에 있는 그림을 보고, 페이지 교체 알고리즘 중 어떤 알고리즘인지 맞추세요.</b></summary>
<div markdown="1">

![image](https://github.com/user-attachments/assets/68936421-1b99-41f5-9b2e-ad046783a4bd)


- 정답: **SCR (Second Chance Replacement, 2차 기회 페이지 교체)**

![image](https://github.com/user-attachments/assets/6e89fbeb-f462-4aae-ae05-0cfe631a05ce)


- 정답: **FIFO (First In First Out)**

</div>
</details>
