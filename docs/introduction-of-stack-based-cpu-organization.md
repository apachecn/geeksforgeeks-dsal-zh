# 基于堆栈的 CPU 组织介绍

> 原文:[https://www . geesforgeks . org/基于堆栈的 cpu 组织介绍/](https://www.geeksforgeeks.org/introduction-of-stack-based-cpu-organization/)

使用基于堆栈的中央处理器组织的计算机基于名为**堆栈**的数据结构。堆栈是数据字的列表。它使用的是**后进先出(LIFO)** 访问方式，这是大多数 CPU 中最流行的访问方式。一个寄存器用于存储堆栈最顶层元素的地址，称为**堆栈指针(SP)** 。在这种组织中，对堆栈数据执行算术逻辑单元操作。这意味着两个操作数在堆栈中都是必需的。操作之后，结果被放入堆栈。

对堆栈的操作者执行的两个主要操作是**推**和**弹出**。这两个操作仅从一端执行。

1.  **Push –**
    This operation results in inserting one operand at the top of the stack and it decrease the stack pointer register. The format of the PUSH instruction is:

    ```
    PUSH 
    ```

    它将指定地址的数据字插入堆栈顶部。它可以实现为:

    ```
    //decrement SP by 1
    SP <-- SP - 1 

    //store the content of specified memory address 
    //into SP; i.e, at top of stack
    SP <-- (memory address) 
    ```

2.  **Pop –**
    This operation results in deleting one operand from the top of the stack and it increase the stack pointer register. The format of the POP instruction is:

    ```
    POP 
    ```

    它将堆栈顶部的数据字删除到指定的地址。它可以实现为:

    ```
    //transfer the content of  SP (i.e, at top most data) 
    //into specified memory location                   
    (memory address) <-- SP

    //increment SP by 1
    SP <-- SP + 1 
    ```

    操作类型指令不需要该 CPU 组织中的地址字段。这是因为操作是对堆栈顶部的两个操作数执行的。例如:

    ```
    SUB 
    ```

    该指令只包含操作码，没有地址字段。它从堆栈中弹出两个最上面的数据，减去数据，然后将结果放入堆栈顶部。

    **PDP-11、英特尔的 8085 和惠普的 3000** 都是堆栈组织计算机的一些例子。

    **基于堆栈的 CPU 组织的优势–**

    *   复杂算术表达式的高效计算。
    *   指令的执行速度很快，因为操作数数据存储在连续的存储单元中。
    *   指令长度很短，因为它们没有地址字段。

    **基于堆栈的 CPU 组织的缺点–**

    *   程序的大小增加了。

    **注:** *基于堆栈的 CPU 组织使用零地址指令。*