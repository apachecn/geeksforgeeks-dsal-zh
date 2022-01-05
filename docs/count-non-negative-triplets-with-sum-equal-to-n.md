# 计数总和等于 N 的非负三胞胎

> 原文:[https://www . geesforgeks . org/count-non-negative-triples-with-sum-equal-n/](https://www.geeksforgeeks.org/count-non-negative-triplets-with-sum-equal-to-n/)

给定一个整数 **N** 。任务是找到非负整数的不同有序三元组(a，b，c)的数量，使得 **a + b + c = N** 。
**例:**

> **输入:** N = 2
> **输出:** 6
> 三元组为:(0，0，2)，(1，0，1)，(0，1，1)，(2，0，0)，(0，2，0)，(1，1，0)
> **输入:** N = 50
> **输出:** 1326

**逼近:**
首先，很容易看出，对于每个非负整数 **N** ，方程 **a + b = N** 可以由 **(N+1)** 不同的有序对 **(a，b)来满足。**现在我们可以将 **c** 值从 **0** 分配给 **N** ，这样就可以找到 **a+b** 的有序对。它将形成一系列 **N+1** 自然数，其和将给出三胞胎的计数。
以下是上述办法的实施:

## C++

```
// CPP program to find triplets count
#include <bits/stdc++.h>
using namespace std;

// Function to find triplets count
int triplets(int N)
{
    // Sum of first n+1 natural numbers
    return ((N + 1) * (N + 2)) / 2;
}

// Driver code
int main()
{
    int N = 50;

    // Function call
    cout << triplets(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find triplets count
class GFG
{

// Function to find triplets count
static int triplets(int N)
{
    // Sum of first n+1 natural numbers
    return ((N + 1) * (N + 2)) / 2;
}

// Driver code
public static void main(String[] args)
{
    int N = 50;

    System.out.println(triplets(N));
}
}

// This code is contributed
// by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find triplets count

# Function to find triplets count
def triplets(N):

    # Sum of first n+1 natural numbers
    return ((N + 1) * (N + 2)) // 2;

# Driver code
N = 50;

# Function call
print(triplets(N))

# This code is contributed by nidhi
```

## C#

```
// C# program to find triplets count
using System;

class GFG
{

// Function to find triplets count
static int triplets(int N)
{
    // Sum of first n+1 natural numbers
    return ((N + 1) * (N + 2)) / 2;
}

// Driver code
public static void Main()
{
    int N = 50;

    Console.WriteLine(triplets(N));
}
}

// This code is contributed
// by anuj_67..
```

## java 描述语言

```
<script>

    // Javascript program to find triplets count   

    // Function to find triplets count
    function triplets(N)
    {
        // Sum of first n+1 natural numbers
        return ((N + 1) * (N + 2)) / 2;
    }

    let N = 50;
    document.write(triplets(N));

</script>
```

**Output:** 

```
1326
```

**时间复杂度:** O(1)