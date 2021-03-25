## Process

프로세스는 *메모리에 올라가 실행중인 프로그램*을 의미한다.<br>
간단하게 지금 실행중인 프로그램이다.

프로그램이 메모리에 올라갈 경우 두개의 영역을 할당받는데, 하나는 PCB(Process Control Block)이고 다른 하나는 주소공간이다.

PCB의 경우 현재 프로세스의 상태나 실행중인 코드가 어디인지 등 프로세스에 대한 정보가 담겨있다.

주소공간의 경우 내부적으로 다시 Code, Heap, Data, Stack 영역으로 나뉜다.<br>
Code영역은 말 그대로 코드가 담겨져 있는 공간이다.<br>
Data영역은 전역변수가 담겨있으며, Heap은 동적할당된 것들이 담겨있다.<br>
Stack의 경우에는 지역변수나 매개변수같이 잠시 사용되었다 사라지는 것들이 담겨있다.

## Thread

스레드는 *하나의 프로세스 내에서 두가지 이상의 흐름을 가지고 싶을 때 사용하는 것*이다.<br>
프로세스의 주소공간 중 코드, Data, Heap 영역은 공유하지만 Stack 영역은 공유하지 않는다.

## 멀티프로세싱 & 멀티스레드

멀티프로세싱은 프로세스가 2개 이상 동시에 작업하여 CPU의 활용을 최대로 하는것을 말한다.

멀티스레드는 하나의 프로세스 내에서 2개 이상의 흐름을 위해 여러 스레드들이 작업하는 것을 말한다.

둘 모두 사용을 하게되면 동시에 여러 작업을 하는것처럼 보이나, 멀티프로세싱은 프로세스가 두개 이상 작동하고, 멀티 스레드는 하나의 프로세스 내부에서 여러 작업을 한다는 차이가 있다.<br>
그리고 context switching 시에도 멀티프로세싱이 비용이 더 많이든다.<br>
왜냐하면 스레드는 code, heap, data는 그대로고 stack 영역만 바꾸면 된다.<br>
하지만 프로세스의 작업을 바꾸려면 위의 모든 영역을 바꿔주어야 한다. 그래서 바꾸는 시간이 더 오래걸린다는 단점이 있다.