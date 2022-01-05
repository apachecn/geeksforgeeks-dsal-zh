# 带幂循环的时间复杂度

> 原文:[https://www . geeksforgeeks . org/带电源的环路时间复杂性/](https://www.geeksforgeeks.org/time-complexity-of-loop-with-powers/)

下面这个函数的时间复杂度是多少？

## C++

```
void fun(int n, int k)
{
    for (int i = 1; i <= n; i++)
    {
        int p = pow(i, k);
        for (int j = 1; j <= p; j++)
        {
            // Some O(1) work
        }
    }
}

// This code is contributed by Shubham Singh
```

## C

```
void fun(int n, int k)
{
    for (int i = 1; i <= n; i++)
    {
        int p = pow(i, k);
        for (int j = 1; j <= p; j++)
        {
            // Some O(1) work
        }
    }
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
static void fun(int n, int k)
{
    for (int i = 1; i <= n; i++)
    {
        int p = Math.pow(i, k);
        for (int j = 1; j <= p; j++)
        {
            // Some O(1) work
        }
    }
}

// This code is contributed by umadevi9616
```

## 蟒蛇 3

```
def fun(n, k):

    for i in range(1, n + 1):
        p = pow(i, k)
        for j in range(1, p + 1):
            # Some O(1) work

# This code is contributed by Shubham Singh
```

## C#

```
static void fun(int n, int k)
{
    for (int i = 1; i <= n; i++)
    {
        int p = Math.Pow(i, k);
        for (int j = 1; j <= p; j++)
        {
            // Some O(1) work
        }
    }
}

// This code is contributed by umadevi9616
```

## java 描述语言

```
<script>

// JavaScript program for the above approach
function fun(n, k)
{
    for(let i = 1; i <= n; i++)
    {
        int p = Math.pow(i, k);
        for (let j = 1; j <= p; j++)
        {
            // Some O(1) work
        }
    }
}

// This code is contributed by Shubham Singh

</script>
```

上述功能的时间复杂度可以写成 1<sup>k</sup>+2<sup>k</sup>+3<sup>k</sup>+…n1<sup>k</sup>。

让我们尝试几个例子:

```
k=1
Sum = 1 + 2 + 3 ... n 
    = n(n+1)/2 
    = n2/2 + n/2

k=2
Sum = 12 + 22 + 32 + ... n12.
    = n(n+1)(2n+1)/6
    = n3/3 + n2/2 + n/6

k=3
Sum = 13 + 23 + 33 + ... n13.
    = n2(n+1)2/4
    = n4/4 + n3/2 + n2/4     
```

一般来说，渐近值可以写成**(n<sup>k+1</sup>)/(k+1)+θ(n<sup>k</sup>)**
如果 n > =k 那么时间复杂度将在**O((n<sup>k+1</sup>)/(k+1)】**中考虑，如果 n < k 那么时间复杂度将在**O(***】T14 中考虑*

如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论