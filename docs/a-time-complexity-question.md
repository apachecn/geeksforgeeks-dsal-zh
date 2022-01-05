# 一个时间复杂度问题

> 原文:[https://www.geeksforgeeks.org/a-time-complexity-question/](https://www.geeksforgeeks.org/a-time-complexity-question/)

跟随 fun()函数的时间复杂度是多少？假设 log(x)返回以 2 为基数的日志值。

## C++

```
void fun()
{
    int i, j;
    for (i = 1; i <= n; i++)
        for (j = 1; j <= log(i); j++)
            cout << "GeeksforGeeks";
}

// This code is contributed by SHUBHAMSINGH10.
```

## C

```
void fun()
{
    int i, j;
    for (i = 1; i <= n; i++)
        for (j = 1; j <= log(i); j++)
            printf("GeeksforGeeks");
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
static void fun()
{
    int i, j;
    for (i = 1; i <= n; i++)
        for (j = 1; j <= log(i); j++)
            System.out.printf("GeeksforGeeks");
}

// This code is contributed by umadevi9616
```

## 蟒蛇 3

```
import math
def fun():
    i = 0
    j = 0
    for i in range(1, n + 1):
        for j in range(1,math.log(i) + 1):
            print("GeeksforGeeks")

# This code is contributed by SHUBHAMSINGH10.
```

## C#

```
static void fun()
{
    int i, j;
    for (i = 1; i <= n; i++)
        for (j = 1; j <= log(i); j++)
            Console.Write("GeeksforGeeks");
}

// This code is contributed by umadevi9616
```

## java 描述语言

```
const fun()
{
    let i, j;
    for (i = 1; i <= n; i++)
        for (j = 1; j <= Math.log(i); j++)
            document.write("GeeksforGeeks");
}

// This code is contributed by SHUBHAMSINGH10.
```

上述函数的时间复杂度可以写成θ(log 1) + θ(log 2) + θ(log 3) +。。。。+ θ(log n)也就是θ(log n！)
log n 的增长顺序对于大的 n 值，即θ(log n！)= θ(n log n)。所以 fun()的时间复杂度是θ(n log n)。
表达式θ(log n！)= θ(n log n)可以很容易地根据[斯特林近似(或斯特林公式)](http://en.wikipedia.org/wiki/Stirling%27s_approximation)推导出来。

```
log n! = n*log n - n = O(n*log(n)) 
```

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。
来源:
T2】http://en.wikipedia.org/wiki/Stirling%27s_approximation