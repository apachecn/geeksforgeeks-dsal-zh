# 检查二进制流中的可分性

> 原文:[https://www . geesforgeks . org/check-可分性-二进制-stream/](https://www.geeksforgeeks.org/check-divisibility-binary-stream/)

二进制数的流来了，任务是告诉到目前为止形成的数是否能被给定的数 n 整除。
在任何给定的时间，你都会得到 0 或 1，并告诉用这些位形成的数是否能被 n 整除。

一般来说，电子商务公司会问这类问题。是微软面试的时候问我的。其实那个问题有点简单，面试官把 n 固定为 3。

<center>**Method 1 (Simple but causes overflow):**</center>

Keep on calculating the number formed and just check divisibility by n.

```
/* Simple implementation of the logic,
   without error handling compiled with
   Microsoft visual studio 2015 */
void CheckDivisibility2(int n)
{
    int num = 0;
    std::cout << "press any key other than"
                " 0 and 1 to terminate \n";
    while (true)
    {
        int incomingBit;

        // read next incoming bit via standard
        // input. 0, 00, 000.. are same as int 0
        // ans 1, 01, 001, 00..001 is same as 1.
        std::cin >> incomingBit;

        // Update value of num formed so far
        if (incomingBit == 1)
            num = (num * 2 + 1);
        else if (incomingBit == 0)
            num = (num * 2);

        else
            break;
        if (num % n == 0)
            std::cout << "yes \n";
        else
            std::cout << "no \n";
    }
}
```

这个解决方案的问题:溢出怎么办。因为 0 和 1 将继续出现，形成的数字将超出整数范围。

<center>**Method 2 (Doesn’t cause overflow) :**</center>

In this solution, we just maintain the remainder if remainder is 0, the formed number is divisible by n otherwise not. This is the same [technique that is used in Automata](https://www.geeksforgeeks.org/dfa-based-division/) to remember the state. Here also we are remembering the state of divisibility of input number.

为了实现这种技术，我们需要观察二进制数的值在被 0 或 1 追加时是如何变化的。

举个例子吧。假设你有二进制数 1。
如果加上 0，它将变成 10(十进制中的 2)表示是前一个值的 2 倍。
如果加 1，将变成 11(小数 3)，是之前值+1 的 2 倍。

**如何帮助得到余数？**
任何数(n)都可以写成 m = an + r 的形式，其中 a、n 和 r 是整数，r 是余数。所以当 m 乘以任何数，余数。假设 m 乘以 x，那么 m 将是 mx = xan + xr。so(MX)% n =(xan)% n+(xr)% n = 0+(xr)% n =(xr)% n；

我们只需要对余数进行上述计算(当数字被 0 或 1 追加时，计算数字的值)。

```
When a binary number is appended by 0 (means 
multiplied by 2), the new remainder can be 
calculated based on current remainder only.
r = 2*r % n;

And when a binary number is appended by 1.
r = (2*r + 1) % n; 
```

```
// C++ program to check divisibility in a stream
#include <iostream>
using namespace std;

/*  A very simple implementation of the logic,
    without error handling. just to demonstrate
    the above theory. This simple version not
    restricting user from typing 000, 00 , 000.. ,
    because this all will be same as 0 for integer
    same is true for 1, 01, 001, 000...001 is same
    as 1, so ignore this type of error handling
    while reading just see the main logic is correct. */
void CheckDivisibility(int n)
{
    int remainder = 0;
    std::cout << "press any key other than 0"
                 " and 1 to terminate \n";
    while (true)
    {
        // Read next incoming bit via standard
        // input. 0, 00, 000.. are same as int 0
        // ans 1, 01, 001, 00..001 is same as 1.
        int incomingBit;
        cin >> incomingBit;

        // Update remainder
        if (incomingBit == 1)
            remainder = (remainder * 2 + 1) % n;
        else if (incomingBit == 0)
            remainder = (remainder * 2) % n;
        else
            break;

        // If remainder is 0.
        if (remainder % n == 0)
            cout << "yes \n";
        else
            cout << "no \n";
    }
}

// Driver code
int main()
{
    CheckDivisibility(3);
    return 0;
}
```

输入:

```
1
0
1
0
1
-1

```

输出:

```
Press any key other than 0 and 1 to terminate 
no 
no 
no 
no 
yes 

```

**相关文章:**
[基于 DFA 的划分](https://www.geeksforgeeks.org/dfa-based-division/)
[检查一个流是否为 3 的倍数](https://www.geeksforgeeks.org/write-an-efficient-method-to-check-if-a-number-is-multiple-of-3/)

本文由**punet**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论