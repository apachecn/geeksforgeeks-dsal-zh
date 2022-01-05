# 分治循环高级主定理

> 原文:[https://www . geeksforgeeks . org/advanced-master-定理用于分治重现/](https://www.geeksforgeeks.org/advanced-master-theorem-for-divide-and-conquer-recurrences/)

[主定理](https://www.geeksforgeeks.org/analysis-algorithm-set-4-master-method-solving-recurrences/)用于根据渐近符号确定算法(分治算法)的运行时间。
考虑一个可以用递归解决的问题。

```
function f(input x size n)
if(n < k)
solve x directly and return 
else
divide x into a subproblems of size n/b
call f recursively to solve each subproblem
Combine the results of all sub-problems

```

上述算法将问题分成 **a** 个子问题，每个子问题的大小为 n/b，并递归求解以计算问题，为问题所做的额外工作由 f(n)给出，即在上述过程中创建子问题并组合其结果的时间。

因此，根据主定理，上述算法的运行时间可以表示为:

```
T(n) = aT(n/b) + f(n) 

```

其中 n =问题的大小
a =递归中的子问题的数量，a > = 1
n/b =每个子问题的大小
f(n) =递归调用之外的工作成本，如划分为子问题以及将它们组合以获得解决方案的成本。

不是所有的递推关系都可以用主定理解决，即如果

*   T(n)不是单调的，例如:T(n) = sin n
*   f(n)不是多项式，例如:T(n) = 2T(n/2) + 2 <sup>n</sup>

该定理是 master 定理的高级版本，如果递归具有以下形式，则可用于确定分治算法的运行时间:-

![Formula to calculate runtime of divide and conquer algorithms](img/292c1ccd69124e068da4d45ac8edf6b7.png)

其中 n =问题的大小
a =递归中子问题的数量，a > = 1
n/b =每个子问题的大小
b > 1，k > = 0，p 为实数。

然后，

1.  如果 a > b <sup>k</sup> ，那么 T(n)=θ(n<sup>log</sup>T4<sup>b</sup>T7<sup>a</sup>
2.  如果 a = b <sup>k</sup> ，那么
    (a)如果 p > -1，那么 T(n)=θ(n<sup>log</sup><sub><sup>b</sup></sub><sup>a</sup>log<sup>p+1</sup>n)
    (b)如果 p = -1，那么 T(n)=θ(n<sup>log</sup><sub>b</sub>T20】a
3.  如果 a < b <sup>k</sup> ，那么
    (a)如果 p > = 0，那么 T(n)=θ(n<sup>k</sup>log<sup>p</sup>n)
    (b)如果 p < 0，那么 T(n) = θ(n <sup>k</sup> )

**时间复杂性分析–**

*   **例-1:二分搜索法–**T(n)= T(n/2)+O(1)
    a = 1，b = 2，k = 0，p = 0
    b <sup>k</sup> = 1。所以，a = b <sup>k</sup> 和 p > -1【案例 2。(a)】
    T(n)=θ(n<sup>log</sup><sub><sup>b</sup></sub>T15】alog<sup>p+1</sup>n)
    T(n)=θ(logn)
*   **示例-2:合并排序–**T(n)= 2T(n/2)+O(n)
    a = 2，b = 2，k = 1，p = 0
    b <sup>k</sup> = 2。所以，a = b <sup>k</sup> 和 p > -1【案例 2。(a)】
    T(n)=θ(n<sup>log</sup><sub><sup>b</sup></sub>T15】alog<sup>p+1</sup>n)
    T(n)=θ(nlogn)
*   **Example-3:** T(n) = 3T(n/2) + n<sup>2</sup> 
    a = 3, b = 2, k = 2, p = 0 
    b<sup>k</sup> = 4\. So, a < b<sup>k</sup> and p = 0 [Case 3.(a)] 
    T(n) = θ(n<sup>k</sup> log<sup>p</sup>n) 
    T(n) = θ(n<sup>2</sup>) 
*   **Example-4:** T(n) = 3T(n/2) + log<sup>2</sup>n 
    a = 3, b = 2, k = 0, p = 2 
    b<sup>k</sup> = 1\. So, a > b<sup>k</sup> [Case 1] 
    T(n) = θ(n<sup>log</sup><sub><sup>b</sup></sub><sup>a</sup> ) 
    T(n) = θ(n<sup>log</sup><sub><sup>2</sup></sub><sup>3</sup>) 
*   **Example-5:** T(n) = 2T(n/2) + nlog<sup>2</sup>n 
    a = 2, b = 2, k = 1, p = 2 
    b<sup>k</sup> = 2\. So, a = b<sup>k</sup> [Case 2.(a)] 
    T(n) = θ(n<sup>log</sup><sub><sup>b</sup></sub><sup>a</sup>log<sup>p+1</sup>n ) 
    T(n) = θ(n<sup>log</sup><sub><sup>2</sup></sub><sup>2</sup>log<sup>3</sup>n) 
    T(n) = θ(nlog<sup>3</sup>n) 
*   **示例-6:**T(n)= 2<sup>n</sup>T(n/2)+n<sup>n</sup>
    由于函数不是 T(n)= aT(n/b)+θ(n<sup>k</sup>log<sup>p</sup>n)
    的形式，因此无法使用上述方法求解此递归

**GATE 练习题–**

*   [GATE-CS-2017(第 2 集)|第 56 题](https://www.geeksforgeeks.org/gate-gate-cs-2017-set-2-question-56/)
*   [GATE IT 2008 |问题 42](https://www.geeksforgeeks.org/gate-gate-it-2008-question-42/)
*   [GATE CS 2009 |第 35 题](https://www.geeksforgeeks.org/gate-gate-cs-2009-question-35/)