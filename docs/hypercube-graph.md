# 超立方体图

> 原文:[https://www.geeksforgeeks.org/hypercube-graph/](https://www.geeksforgeeks.org/hypercube-graph/)

给你的输入是 n 阶图(连接到一个节点的最高边数)，你必须找到 n 阶超立方体图的顶点数。

**例:**

```
Input : n = 3
Output : 8

Input : n = 2
Output : 4
```

在超立方体图 Q(n)中，n 代表图的度。超立方体图表示一个图可以连接的最大边数，使其成为 n 度图，每个顶点都有相同的 n 度，在该表示中，只增加固定数量的边和顶点，如下图所示:

![Hypercube Graph](img/397e7fc171f7c4fa7bc2e8dc42f750da.png)

所有超立方体图都是哈密尔顿的，**n 阶超立方体图有(2^n)个顶点，**，对于输入 n 为阶的图我们要求相应的 2 的幂。

## C++

```
// C++ program to find vertices in a hypercube 
// graph of order n
#include <iostream>
using namespace std;

// function to find power of 2
int power(int n)
{
    if (n == 1)
        return 2;
    return 2 * power(n - 1);
}

// driver program
int main()
{
    // n is the order of the graph
    int n = 4;
    cout << power(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find vertices in 
// a hypercube graph of order n 
class GfG
{

    // Function to find power of 2 
    static int power(int n) 
    { 
        if (n == 1) 
            return 2; 
        return 2 * power(n - 1); 
    } 

    // Driver program 
    public static void main(String []args)
    {

        // n is the order of the graph 
        int n = 4;
        System.out.println(power(n));
    }
}

// This code is contributed by Rituraj Jain
```

## 蟒蛇 3

```
# Python3 program to find vertices in a hypercube 
#  graph of order n

# function to find power of 2
def power(n):
    if n==1:
        return 2
    return 2*power(n-1)

# Dricer code
n =4
print(power(n))

# This code is contributed by Shrikant13
```

## C#

```
// C# program to find vertices in 
// a hypercube graph of order n 
using System;

class GfG
{

    // Function to find power of 2 
    static int power(int n) 
    { 
        if (n == 1) 
            return 2; 
        return 2 * power(n - 1); 
    } 

    // Driver code 
    public static void Main()
    {

        // n is the order of the graph 
        int n = 4;
        Console.WriteLine(power(n));
    }
}

// This code is contributed by Mukul Singh
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find vertices in 
// a hypercube graph of order n 
{

    // Function to find power of 2 
    function power($n) 
    { 
        if ($n == 1) 
            return 2; 
        return 2 * power($n - 1); 
    } 

    // Driver Code
    {

        // n is the order of the graph 
        $n = 4;
        echo(power($n));
    }
}

// This code is contributed by Code_Mech
?>
```

## java 描述语言

```
<script>

// Javascript program to find vertices in a hypercube 
// graph of order n

// function to find power of 2
function power(n)
{
    if (n == 1)
        return 2;
    return 2 * power(n - 1);
}

// driver program
// n is the order of the graph
var n = 4;
document.write( power(n));

</script>
```

**输出:**

```
16
```