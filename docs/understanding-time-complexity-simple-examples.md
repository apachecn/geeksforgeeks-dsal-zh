# 用简单的例子理解时间复杂度

> 原文:[https://www . geeksforgeeks . org/了解-时间-复杂性-简单-示例/](https://www.geeksforgeeks.org/understanding-time-complexity-simple-examples/)

很多学生在理解时间复杂性的概念时会感到困惑，但在本文中，我们将用一个非常简单的例子来解释:
想象一个有 100 名学生的教室，你把笔交给一个人。现在，你想要那支笔。这里有一些找到笔的方法，以及 O 的顺序是什么。
**O(n <sup>2</sup> ):** 你去问问班里第一个人，他有笔没有。还有，你问这个人教室里其他 99 个人有没有那支笔等等，
这就是我们所说的 O(n <sup>2</sup> )。
**O(n):** 单独去问每个学生就是 O(n)。
**O(log n):** 现在我把班级分成两组，然后问:“是在教室的左边，还是右边？”然后我把那个小组分成两个，再问一遍，以此类推。重复这个过程，直到只剩下一个学生拿着你的笔。这就是你说的 O(对数 n)的意思。
如果只有一个学生知道笔藏在哪个学生身上，我可能需要进行 O(n <sup>2</sup> )搜索。如果有一个学生有笔，而且只有他们知道，我会用 O(n)。如果所有的学生都知道，我会使用 O(log n)搜索，但只有在我猜对了的情况下才会告诉我。

**注:**我们对程序执行期间输入的时间增长率感兴趣。

**另一个例子:**
算法/代码的时间复杂度是**而不是**等于执行特定代码所需的实际时间，而是语句执行的次数。我们可以用时间命令来证明这一点。例如，用 C/C++或任何其他语言编写代码来查找 N 个数字之间的最大值，其中 N 从 10、100、1000、10000 不等。并使用以下命令在基于 Linux 操作系统(Fedora 或 Ubuntu)上编译代码:

```
gcc program.c – o program
run it with time ./program
```

您将获得令人惊讶的结果，即对于 N = 10，您可能获得 0.5 毫秒的时间，对于 N = 10，000，您可能获得 0.2 毫秒的时间。此外，您将在不同的机器上获得不同的计时。因此，我们可以说执行代码所需的实际时间取决于机器(无论您使用的是 pentium1 还是 pentium5)，如果您的机器在局域网/广域网中，它还会考虑网络负载。甚至你不会在同一台机器上用同样的代码得到同样的计时，这背后的原因是当前的网络负载。
现在，问题出现了，如果时间复杂度不是执行代码所需的实际时间，那么它是什么？

**答案是:**我们考虑的不是执行代码中每条语句所需的实际时间，而是每条语句执行的次数。
例如:

## C

```
#include <stdio.h>
int main()
{
    printf("Hello World");
}
```

**Output**

```
Hello World
```

在上面的代码“你好世界！！!"在屏幕上只打印一次。因此，时间复杂度是恒定的:O(1)即每次执行代码需要恒定的时间量，无论您使用的是哪种操作系统或哪种机器配置。

**现在考虑另一个代码:**

## C

```
#include <stdio.h>
void main()
{
    int i, n = 8;
    for (i = 1; i <= n; i++) {
        printf("Hello Word !!!\n");
    }
}
```

**Output**

```
Hello Word !!!
Hello Word !!!
Hello Word !!!
Hello Word !!!
Hello Word !!!
Hello Word !!!
Hello Word !!!
Hello Word !!!
```

在上面的代码“你好世界！！!"会打印 N 次。所以，上述代码的时间复杂度为 O(N)。
来源: [Reddit](https://www.reddit.com/r/programming/comments/1f2ml3/what_does_olog_n_mean_exactly/)

**附加信息:**
例如:
让我们考虑具有以下规格的模型机器:
–单处理器
–32 位
–顺序执行
–1 单位时间用于算术和逻辑运算
–1 单位时间用于赋值和返回语句

**1。两个数之和:**

## C

```
Pseudocode:
Sum(a,b){
return a+b  //Takes 2 unit of time(constant) one for arithmetic operation and one for return.(as per above conventions)   cost=2 no of times=1
}
```

**Tsum= 2 = C =O(1)**

**2。列表所有元素的总和:**

## C

```
Pseudocode:
list_Sum(A,n){//A->array and n->number of elements in the array
total =0           // cost=1  no of times=1
for i=0 to n-1     // cost=2  no of times=n+1 (+1 for the end false condition)
sum = sum + A[i]   // cost=2  no of times=n 
return sum         // cost=1  no of times=1
}         
```

**Tsum = 1+2 *(n+1)+2 * n+1 = 4n+4 = C1 * n+C2 = O(n)**

**3。矩阵所有元素之和:**

对于这一个，复杂度是多项式方程(平方矩阵的二次方程)
**矩阵 nxn =>Tsum = an<sup>2</sup>+bn+c**
**对于这一个 Tsum，如果按照 n<sup>2</sup>= O(n<sup>2</sup>)**
**的顺序，上述代码不在 IDE 中运行，因为它们是伪代码，不像任何编程语言。**
因此，从上面我们可以得出结论，执行时间随着我们使用输入进行的操作类型而增加。
上面的 O - >叫做大–Oh，是一个渐近符号。还有其他渐近符号，如θ和欧姆。

**如何比较算法？**

为了比较算法，让我们定义几个客观的度量:

*   **执行时间:** *这不是一个好的衡量标准，因为执行时间是特定于特定计算机的。*
*   **执行的语句数量:**这不是一个好的衡量标准，因为语句的数量会随着编程语言以及单个程序员的风格而变化。
*   **理想解:**假设我们将给定算法的运行时间表示为输入大小 n(即 f(n))的函数，并比较这些不同函数对应的运行时间。这种比较与机器时间、编程风格等无关。

**你可以参考:** [**阅读关于渐近符号**](https://www.geeksforgeeks.org/analysis-of-algorithems-little-o-and-little-omega-notations/)
本文作者提供的附加信息是 **Pathange Balaji Rao。**