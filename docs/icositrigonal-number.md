# icositrigonical 号

> 原文:[https://www.geeksforgeeks.org/icositrigonal-number/](https://www.geeksforgeeks.org/icositrigonal-number/)

给定一个数字 **N** ，任务是找到 **N <sup>第</sup>T5【Icositrigonal】号。** 

> 一个整数是一类整数。它有一个 23 边的多边形，叫做 Icositrigon。第 N 个 Icositrigonal 数字计数是 23 个点的数量，所有其他点都被一个公共的共享角包围并形成一个图案。前几个 Icositrigonol 数字是 **1、23、66、130、215、321、448……**

**例:**

> **输入:** N = 2
> **输出:** 23
> **解释:**
> 第二个 Icositrigonol 数是 66。
> **输入:** N = 6
> **输出:** 321

**方法:**第 N 个 Icositrigonal 数由公式给出:

以下是上述方法的实现:

## C++

```
// C++ program to find nth
// Icositrigonal number

#include <bits/stdc++.h>
using namespace std;

// Function to find N-th
// Icositrigonal number
int Icositrigonal_num(int n)
{
    // Formula to calculate nth
    // Icositrigonal number
    return (21 * n * n - 19 * n) / 2;
}

// Driver Code
int main()
{
    int n = 3;
    cout << Icositrigonal_num(n) << endl;

    n = 10;
    cout << Icositrigonal_num(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find nth
// Icositrigonal number
class GFG{

// Function to find N-th
// Icositrigonal number   
static int IcositrigonalNum(int n)
{

    // Formula to calculate nth
    // Icositrigonal number
    return (21 * n * n - 19 * n) / 2;
}

// Driver code
public static void main(String[] args)
{
    int n = 3;
    System.out.print(IcositrigonalNum(n) + "\n");

    n = 10;
    System.out.print(IcositrigonalNum(n));
}
}

// This code is contributed by spp____
```

## 蟒蛇 3

```
# Python3 program to find nth
# Icositrigonal number

# Function to find N-th
# Icositrigonal number
def IcositrigonalNum(n):

    # Formula to calculate nth
    # Icositrigonal number
    return (21 * n * n - 19 * n) / 2;

# Driver code
n = 3
print(IcositrigonalNum(n))

n = 10
print(IcositrigonalNum(n))

# This code is contributed by spp____
```

## C#

```
// C# program to find nth
// Icositrigonal number
using System;

class GFG{

// Function to find N-th
// Icositrigonal number    
static int IcositrigonalNum(int n)
{

    // Formula to calculate nth
    // Icositrigonal number
    return (21 * n * n - 19 * n) / 2;
}

// Driver code
public static void Main()
{
    int n = 3;
    Console.WriteLine(IcositrigonalNum(n));

    n = 10;
    Console.WriteLine(IcositrigonalNum(n));
}
}

// This code is contributed by spp____
```

## java 描述语言

```
<script>

    // Javascript program to find nth 
    // Icositrigonal number

    // Function to find N-th 
    // Icositrigonal number 
    function Icositrigonal_num(n) 
    { 
        // Formula to calculate nth 
        // Icositrigonal number 
        return (21 * n * n - 19 * n) / 2; 
    } 

    let n = 3; 
    document.write(Icositrigonal_num(n) + "</br>"); 

    n = 10; 
    document.write(Icositrigonal_num(n));

</script>
```

**Output:** 

```
66
955
```

**参考:**T2】https://en.wikipedia.org/wiki/Polygonal_number