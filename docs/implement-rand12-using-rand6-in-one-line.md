# 在一行中使用 rand6()实现 rand12()

> 原文:[https://www . geeksforgeeks . org/implement-rand 12-using-rand 6-in-line/](https://www.geeksforgeeks.org/implement-rand12-using-rand6-in-one-line/)

给定一个以相等概率从 1 到 6 返回随机数的函数 rand6()，使用以相等概率从 1 到 12 返回随机数的 rand6()实现一个线性函数 rand12()。解决方案应尽量减少对 rand6()方法的调用次数。不允许使用任何其他库函数和浮点运算。

想法是使用表达式 **rand6() + (rand6() % 2) * 6** 。它以相等的概率返回从 1 到 12 的随机数。表达式相当于–

```
// if rand6() is even
if (rand6() % 2)
    return 6 + rand6();
else // if rand6() is odd
    return rand6();

```

我们也可以使用以下任何一个以类似方式工作的表达式–

*   **rand6() +！(rand6() % 2) * 6** 或
*   **rand6() + (rand6() & 1) * 6** 或
*   **边缘 6() +！(边缘 6() & 1) * 6**

以下是上述想法的 C++实现–

```
// C++ Program to print random numbers from 1 to 12
// with equal probability using a function that returns
// random numbers from 1 to 6 with equal probability
#include <iostream>
using namespace std;

// Function that returns random numbers from 1 to 6
// with equal probability
int rand6()
{
    // rand() will generate random numbers between 0 and
    // RAND_MAX with equal probability
    // rand() % 6 returns number from 0 to 5 equal probability
    // (rand() % 6) + 1 returns number from 1 to 6 with
    // equal probability
    return (rand() % 6) + 1;
}

// The function uses rand6() to return random numbers
// from 1 to 12 with equal probability
int rand12()
{
    return rand6() + (rand6() % 2) * 6;
}

// Driver code to test above functions
int main()
{
    // Initialize random number generator
    srand(time(NULL));
    int N = 12;

    int freq[N + 1] = { 0 };

    // call rand12() multiple times and store its results
    for (int i = 0; i < N * 100000; i++)
        freq[rand12()]++;

    // print frequency of numbers 1-12
    for (int i = 1; i <= N; i++)
        cout << freq[i] << " ";

    return 0;
}
```

输出:

```
100237 100202 99678 99867 100253 99929 100287 100449 99827 99298 100019 99954 

```

**另一种解决方案–**

```
int rand12()
{
    return (rand6() * 2) - (rand6() & 1);
}

```

**rand6() * 2** 将以相等的概率返回偶数 2、4、6、8、10 和 12， **rand6() & 1** 将分别基于 rand6()是偶数还是奇数返回 0 或 1。因此，表达式**(rand6()* 2)–(rand6()&1)**将以相等的概率返回从 1 到 12 的随机数。

*请注意，以上解决方案在我们每次运行时都会产生不同的结果。*

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。