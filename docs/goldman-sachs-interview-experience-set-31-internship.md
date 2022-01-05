# 高盛面试经历|第 31 集(针对实习)

> 原文:[https://www . geesforgeks . org/Goldman-Sachs-面试-经验-设定-31-实习/](https://www.geeksforgeeks.org/goldman-sachs-interview-experience-set-31-internship/)

Goldman SachsThese are the CS questions asked in the written round of GS in this year’s campus internship.

*   There are 36 horses. We have to find out the fastest 3 horses. In one race, maximum 6 horses can run. How many races are required in minimum to get the result without using a stopwatch?

    我们可以先做 6 场比赛，取 6-6 匹马，在每场比赛中得到最快的马。
    A1、A2、A3、A4、A5、A6
    B1、B2、B3、B4、B5、B6
    C1、C2、C3、C4、C5、C6
    D1、D2、D3、D4、D5、D6
    E1、E2、E3、E4、E5、E6
    F1、F2、F3、F4、F5、F6
    此处 A1>A2>A3>A4>A5>A6，其他同法。
    现在让我们在每场比赛中选择最快的马，然后在它们之间进行一场比赛。让成绩为 A1>B1>C1>D1>E1>F1。我们得到最快的马(A1)。
    现在我们需要找到第二和第三快的马。第二个位置的可用马匹是 B1 和 A2，第三个位置的可用马匹是 A3、B2 和 C1。其他所有的马都不能进入前 3。让这些马进行一场比赛，前 2 名将分别是第 2 名和第 3 名最快的马。
    **所以一共需要 8 场比赛。**

*   Which [data structure](https://www.geeksforgeeks.org/data-structures/) is best suited to [find the median of running stream of numbers](https://www.geeksforgeeks.org/median-of-stream-of-integers-running-integers/) (online algorithm )

    **[堆](https://www.geeksforgeeks.org/heap-data-structure/)**
    的思路是用 max 堆和 min 堆分别存储比当前中位数低一半和比当前中位数大一半的元素。对于每个输入，堆中的元素数量最多相差 1 个元素。当两个堆包含相同数量的元素时，我们选择平均值作为中值，否则我们从包含更多元素的堆中选择中值。
    更多详情请参考[此处](https://www.geeksforgeeks.org/median-of-stream-of-integers-running-integers/)。

*   There are N people in a party, they might or might not know each other names.
    There is a celebrity in the group, celebrity does not know anyone and all people know the celebrity.We can only ask questions like “does A know B?”. **([Celebrity problem](https://www.geeksforgeeks.org/the-celebrity-problem/))**
    What is the worst case time complexity of the optimal solution to find the celebrity?

    **O(n)**
    假设我们问“A 认识 B 吗？”。如果 A 认识 B，A 就不可能是名人。如果甲不认识乙，那么乙不可能是名人。所以每个问题之后，我们可以拒绝一个人。因此，我们需要问最多 n 个问题来正确地计算名人。
    更多详情请参考[此处](https://www.geeksforgeeks.org/the-celebrity-problem/)。

*   给定两个字符串 A 和 B，返回一个字符串，其中 A 和 B 中的字符按照与以 A 中的字符开头的原始字符串相同的顺序交替填充，例如 A =“你好”，B=“再见”，那么输出应该是“HBeylelo”。(|A|，|B|<25000)

创建一个新的空字符串。运行一个最小循环(|A|，|B|)次，然后在答案字符串中添加字符 A 和字符 B。最后，将字符串 A 或 B 的剩余部分追加到应答字符串中。

*   Given a number N find the number of ways to write N as a sum of two or more positive consecutive integers for if N is 7 example there is just 1 way, that is 3+4\. (0<N<10^12)

    假设我们从 1 开始求和，即 1+2+3+…..
    求和小于或等于 N 的最大数:地板(X)
    其中 **X*(X+1)/2=N**
    所以 N 作为连续正整数的和最多由 X 个数组成。
    这里我们可以检查 2 和 X(包括两者)之间的每个可能性 k(假设),为了检查，我们可以使用 A.P 的概念，因为求和系列是 A.P，其和为 N。
    我们知道 A.P，n: k 中的项数
    A . P，S: N 的和
    公共差，d: 1
    我们可以很容易地计算第一项 A，使用公式:

    ```
            S=n/2*(2a + (n-1)d)
    ```

    如果 a 是整数，那么 N 可以表示为 k 个连续整数的和，否则，这是不可能的。当 a 是整数时，计算出现的次数，这就是我们的答案。
    *时间复杂度:*循环运行 X 次，也就是 O(sqrt(N))，在每次迭代中，我们取 O(1)次。所以整体时间复杂度是 **O(sqrt(N))** 。

    页（page 的缩写）s:笔试还包含与**ML****T3【QuantT5】相关的问题。**

    如果你喜欢极客博客并想投稿，你也可以用 contribute.geeksforgeeks.org 写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

    如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。