# 算法分析|第五集(练习题)

> 原文:[https://www . geesforgeks . org/analysis-algorithms-set-5-practice-problems/](https://www.geeksforgeeks.org/analysis-algorithms-set-5-practice-problems/)

我们在之前的文章中讨论了[渐近分析](https://www.geeksforgeeks.org/analysis-of-algorithms-set-1-asymptotic-analysis/)、[最坏、平均和最佳情况](https://www.geeksforgeeks.org/analysis-of-algorithms-set-2-asymptotic-analysis/)、[渐近符号](https://www.geeksforgeeks.org/analysis-of-algorithms-set-3asymptotic-notations/)和[循环分析](https://www.geeksforgeeks.org/analysis-of-algorithms-set-4-analysis-of-loops/)。
本文讨论算法分析的实践问题。
**问题 1:找到下面递归的复杂度:**

```
         { 3T(n-1), if n>0,
T(n) =   { 1, otherwise
```

**解决方案:**

```
Let us solve using substitution.
T(n) = 3T(n-1)
     = 3(3T(n-2)) 
     = 32T(n-2)
     = 33T(n-3)
       ...
       ...
     = 3nT(n-n)
     = 3nT(0) 
     = 3n
This clearly shows that the complexity 
of this function is O(3n).
```

**问题 2:求递归的复杂度:**

```
        { 2T(n-1) - 1, if n>0,
T(n) =   { 1, otherwise
```

**解决方案:**

```
Let us try solving this function with substitution.
T(n) = 2T(n-1) - 1
     = 2(2T(n-2)-1)-1 
     = 22(T(n-2)) - 2 - 1
     = 22(2T(n-3)-1) - 2 - 1 
     = 23T(n-3) - 22 - 21 - 20
       .....
       .....
     = 2nT(n-n) - 2n-1 - 2n-2 - 2n-3
       ..... 22 - 21 - 20

     = 2n - 2n-1 - 2n-2 - 2n-3
       ..... 22 - 21 - 20
     = 2n - (2n-1) 
[Note: 2n-1 + 2n-2 + ...... +  20 = 2n - 1]
T(n) = 1
Time Complexity is O(1). Note that while 
the recurrence relation looks exponential
the solution to the recurrence relation 
here gives a different result.
```

**问题 3:找到下面程序的复杂度:**

## 卡片打印处理机（Card Print Processor 的缩写）

```
function(int n)
{
    if (n==1)
       return;
    for (int i=1; i<=n; i++)
    {
        for (int j=1; j<=n; j++)
        {
            printf("*");
            break;
        }
    }
}
```

**解决方案:**考虑以下函数中的注释。

## 卡片打印处理机（Card Print Processor 的缩写）

```
function(int n)
{
    if (n==1)
       return;
    for (int i=1; i<=n; i++)
    {
        // Inner loop executes only one
        // time due to break statement.
        for (int j=1; j<=n; j++)
        {
            printf("*");
            break;
        }
    }
}
```

上述函数 O(n)的时间复杂度。即使内部循环以 n 为界，但由于 break 语句，它只执行一次。

**问题 4:找到下面程序的复杂性:**

## 卡片打印处理机（Card Print Processor 的缩写）

```
void function(int n)
{
    int count = 0;
    for (int i=n/2; i<=n; i++)
        for (int j=1; j<=n; j = 2 * j)
            for (int k=1; k<=n; k = k * 2)
                count++;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
static void function(int n)
{
    int count = 0;
    for (int i = n / 2; i <= n; i++)
        for (int j = 1; j <= n; j = 2 * j)
            for (int k = 1; k <= n; k = k * 2)
                count++;
}

// This code is contributed by rutvik_56.
```

## C#

```
static void function(int n)
{
    int count = 0;
    for (int i = n / 2; i <= n; i++)
        for (int j = 1; j <= n; j = 2 * j)
            for (int k = 1; k <= n; k = k * 2)
                count++;
}

// This code is contributed by pratham76.
```

**解决方案:**考虑以下函数中的注释。

## 卡片打印处理机（Card Print Processor 的缩写）

```
void function(int n)
{
    int count = 0;
    for (int i=n/2; i<=n; i++)

        // Executes O(Log n) times
        for (int j=1; j<=n; j = 2 * j)

            // Executes O(Log n) times
            for (int k=1; k<=n; k = k * 2)
                count++;
}
```

上述函数的时间复杂度 O(n log <sup>2</sup> n)。

**问题 5:找到下面程序的复杂性:**

## 卡片打印处理机（Card Print Processor 的缩写）

```
void function(int n)
{
    int count = 0;
    for (int i=n/2; i<=n; i++)
        for (int j=1; j+n/2<=n; j = j++)
            for (int k=1; k<=n; k = k * 2)
                count++;
}
```

**解决方案:**考虑以下函数中的注释。

## 卡片打印处理机（Card Print Processor 的缩写）

```
void function(int n)
{
    int count = 0;

    // outer loop executes n/2 times
    for (int i=n/2; i<=n; i++)

        // middle loop executes  n/2 times
        for (int j=1; j+n/2<=n; j = j++)

            // inner loop executes logn times
            for (int k=1; k<=n; k = k * 2)
                count++;
}
```

上述函数的时间复杂度为 0(n<sup>2</sup>logn)。

**问题 6:找到下面程序的复杂性:**

## 卡片打印处理机（Card Print Processor 的缩写）

```
void function(int n)
{
    int i = 1, s =1;
    while (s <= n)
    {
        i++;
        s += i;
        printf("*");
    }
}
```

**解:**我们可以根据关系 s <sub>i</sub> = s <sub>i-1</sub> + i 来定义术语‘s’，每次迭代‘I’的值增加一。在第 i <sup>次</sup>迭代中包含在“s”中的值是第一个“I”正整数的和。如果 k 是程序的总迭代次数，那么 while 循环在以下情况下终止:1 + 2 + 3 …+ k = [k(k+1)/2] > n So k = O(√n)。
上述函数 O 的时间复杂度(√n)。

**问题 7:在下面程序的复杂度上找到一个紧的上限:**

## 卡片打印处理机（Card Print Processor 的缩写）

```
void function(int n)
{
    int count = 0;
    for (int i=0; i<n; i++)
        for (int j=i; j< i*i; j++)
            if (j%i == 0)
            {
                for (int k=0; k<j; k++)
                    printf("*");
            }
}
```

**解决方案:**考虑以下函数中的注释。

## 卡片打印处理机（Card Print Processor 的缩写）

```
void function(int n)
{
    int count = 0;

    // executes n times
    for (int i=0; i<n; i++)

        // executes O(n*n) times.
        for (int j=i; j< i*i; j++)
            if (j%i == 0)
            {
                // executes j times = O(n*n) times
                for (int k=0; k<j; k++)
                    printf("*");
            }
}
```

上述函数的时间复杂度 O(n <sup>5</sup> )。

本文由 Somesh Awasthi 先生供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。