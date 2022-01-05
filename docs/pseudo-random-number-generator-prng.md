# 伪随机数发生器(PRNG)

> 原文:[https://www . geesforgeks . org/伪随机数生成器-prng/](https://www.geeksforgeeks.org/pseudo-random-number-generator-prng/)

**伪随机数发生器(PRNG)** 是指使用数学公式产生随机数序列的算法。PRNGs 生成一系列近似于随机数性质的数字。

PRNG 使用**种子状态**从任意开始状态开始。许多数字是在短时间内生成的，如果序列的起点已知，也可以在以后重现。因此，这些数字是**确定而有效的**。

我们为什么需要 PRNG？

随着计算机的出现，程序员认识到需要一种方法将随机性引入计算机程序。然而，尽管看起来令人惊讶，但很难让计算机偶然做某事，因为计算机盲目地遵循给定的指令，因此是完全可预测的。从像计算机这样确定性的东西中生成真正的随机数是不可能的，所以 PRNG 是一种利用计算机生成随机数的技术。

**PRNG 是如何运作的？**

[线性同余生成器](https://en.wikipedia.org/wiki/Linear_congruential_generator)是生成伪随机数最常见、最古老的算法。生成器由递归关系定义:

```
X<sub>n+1</sub> = (aX<sub>n</sub> + c) mod m
where X is the sequence of pseudo-random values
m, 0 < m  - modulus 
a, 0 < a < m  - multiplier
c, 0 ≤ c < m  - increment
x0, 0 ≤ x0 < m  - the seed or start value
```

我们使用前面的随机整数、整数常数和整数模生成下一个随机整数。要开始，该算法需要一个初始种子，它必须通过某种方式提供。随机性的出现是通过执行**模运算提供的。**。

**PRNG 特色**

*   **高效:** PRNG 可以在短时间内产生很多数字，对于需要很多数字的应用非常有利
*   **确定性的:**如果序列中的起点已知，给定的数字序列可以在以后的某个日期重现。如果您需要在稍后阶段再次重放相同的数字序列，决定论会很方便。
*   **周期性:** PRNGs 是周期性的，这意味着序列最终会自我重复。虽然周期性很难成为理想的特征，但现代 PRNGs 的周期很长，在大多数实际应用中可以忽略

**PRNG 的应用**

PRNGs 适用于需要许多随机数的应用，以及同一序列可以轻松重放的应用。这种应用的流行例子是**模拟和建模应用**。PRNGs 不适合那些数字确实不可预测的重要应用，例如**数据加密和赌博。**

**使用 [srand()](https://www.geeksforgeeks.org/rand-and-srand-in-ccpp/) 的伪随机数发生器**

```
#include<stdio.h>
#include<stdlib.h>
#include<time.h>

int main()
{
   srand(time(NULL));
   int i;

   for(i = 0; i<5; i++)
  printf("%d\t", rand()%10);
}
```

**产出 1:**

```
3  7  0  9  8 
```

**产出 2:**

```
7  6  8  1  4 
```

****说明:** srand()设置种子，rand()使用该种子生成随机数。**时间(空)**从**1971 年 1 月 1 日**返回第二个数字，也就是说，每次我们运行程序，我们有几秒钟的差异，这给程序新的种子。**

****广泛使用的 PRNG 算法** : [滞后斐波那契发生器](https://en.wikipedia.org/wiki/Lagged_Fibonacci_generator)、[线性反馈移位寄存器](https://en.wikipedia.org/wiki/Linear-feedback_shift_register)、 [Blum Blum Shub](https://en.wikipedia.org/wiki/Blum_Blum_Shub) 。**

**[随机数测验](https://www.geeksforgeeks.org/output-c-programs-set-33-rand-srand/)**

**本文由**雅什辛拉**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。**

**如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。**