# 操作系统

#### 1. CPU

##### 目态、管态

大多数计算机系统将 CPU 执行状态分为目态和管态。CPU 的状态属于程序状态字 PSW 的一位。CPU 交替执行操作系统程序和用户程序。

-   管态，又叫特权态、核心态或系统态。CPU 在管态下可以执行指令系统的全集。通常，操作系统在管态下运行。
-   目态，又叫常态、用户态。机器处于目态时，程序只能执行非特权指令。用户程序只能在目态下运行，如果用户程序在目态下执行特权指令，硬件将发生中断，由操作系统获得控制，特权指令执行被禁止，这样可以防止用户程序有意或无意的破坏系统。
-   从目态转换为管态的唯一途径是中断。
-   从管态到目态可以通过修改程序状态字来实现，这将伴随着这由操作系统程序到用户程序的转换。

##### 用户态、内核态

-   当一个任务（进程）执行系统调用而陷入内核代码中执行时，称进程处于内核运行态（内核态）。此时 CPU 处于特权级最高的（0 级）内核代码中执行。当进程处于内核态时，执行的内核代码会使用当前进程的内核栈。每个进程都有自己的内核栈。
-   当进程在执行用户自己的代码时，称其处于用户运行态（用户态）。此时 CPU 在特权级最低的（3 级）用户代码中执行。当正在执行用户程序而突然被中断程序中断时，此时用户程序也可以象征性的称为处于进程的内核态，因为中断处理程序将使用当前进程的内核栈。
-   用户态与内核态的切换：当进程运行在用户态，无论发生中断、异常、系统调用（本质是中断），都会通过异常向量表进入系统状态（内核态），执行完中断服务程序时又恢复原状，返回到用户态。