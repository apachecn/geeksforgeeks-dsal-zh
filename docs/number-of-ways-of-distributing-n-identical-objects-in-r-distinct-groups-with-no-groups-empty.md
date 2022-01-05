# 将 N 个相同的对象分布在 R 个不同的组中而没有空组的方式数

> 原文:[https://www . geesforgeks . org/分发 n 个相同对象的方式数-r-distinct-group-with-no-group-empty/](https://www.geeksforgeeks.org/number-of-ways-of-distributing-n-identical-objects-in-r-distinct-groups-with-no-groups-empty/)

给定两个整数 **N** 和 **R** ，任务是计算将 **N** 相同的对象分配到 **R** 不同的组中的方法数量，使得没有组是空的。

**示例:**

> **输入:** N = 4，R = 2
> **输出:** 3
> 第一组对象数量= 1，第二组对象数量= 3
> 第一组对象数量= 2，第二组对象数量= 2
> 第一组对象数量= 3，第二组对象数量= 1
> 
> **输入:** N = 5，R = 3
> T3】输出: 6

**方法:**思路是用多项式定理。假设**x<sub>1</sub>T5】物体放在第一组，**x<sub>2</sub>T9】物体放在第二组，**x<sub>R</sub>T13】物体放在**R<sup>th</sup>T17】组。给出的是，
**x<sub>1</sub>+x<sub>2</sub>+x<sub>3</sub>+…+x<sub>R</sub>= N**对于所有 **x <sub>i</sub> ≥ 1** 对于 1 ≤ i ≤ R
现在将每一个**x<sub>I</sub>T37】替换为 **y <sub>i 现在所有的 **y** 变量都大于等于零。
等式变为:
**y<sub>1</sub>+y<sub>2</sub>+y<sub>3</sub>+…+y<sub>R</sub>+R = N**对于所有 **y <sub>i</sub> ≥ 0** 对于 1≤I≤R
**y<sub>1</sub>+y<sub>2</sub>+ 其解为**<sup>(N–R)+R–1</sup>C<sub>R–1</sub>**。
这个方程的解由**<sup>N–1</sup>C<sub>R–1</sub>**给出。**</sub>************

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the
// value of ncr effectively
int ncr(int n, int r)
{

    // Initialize the answer
    int ans = 1;

    for (int i = 1; i <= r; i += 1) {

        // Divide simultaneously by
        // i to avoid overflow
        ans *= (n - r + i);
        ans /= i;
    }
    return ans;
}

// Function to return the number of
// ways to distribute N identical
// objects in R distinct objects
int NoOfDistributions(int N, int R)
{
    return ncr(N - 1, R - 1);
}

// Driver code
int main()
{
    int N = 4;
    int R = 3;

    cout << NoOfDistributions(N, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.io.*;

class GFG
{

    // Function to return the
    // value of ncr effectively
    static int ncr(int n, int r)
    {

        // Initialize the answer
        int ans = 1;

        for (int i = 1; i <= r; i += 1)
        {

            // Divide simultaneously by
            // i to avoid overflow
            ans *= (n - r + i);
            ans /= i;
        }
        return ans;
    }

    // Function to return the number of
    // ways to distribute N identical
    // objects in R distinct objects
    static int NoOfDistributions(int N, int R)
    {
        return ncr(N - 1, R - 1);
    }

    // Driver code
    public static void main (String[] args)
    {

        int N = 4;
        int R = 3;

        System.out.println(NoOfDistributions(N, R));
    }
}

// This code is contributed by ajit
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to return the
# value of ncr effectively
def ncr(n, r):

    # Initialize the answer
    ans = 1

    for i in range(1,r+1):

        # Divide simultaneously by
        # i to avoid overflow
        ans *= (n - r + i)
        ans //= i

    return ans

# Function to return the number of
# ways to distribute N identical
# objects in R distinct objects
def NoOfDistributions(N, R):

    return ncr(N - 1, R - 1)

# Driver code

N = 4
R = 3

print(NoOfDistributions(N, R))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to return the
    // value of ncr effectively
    static int ncr(int n, int r)
    {

        // Initialize the answer
        int ans = 1;

        for (int i = 1; i <= r; i += 1)
        {

            // Divide simultaneously by
            // i to avoid overflow
            ans *= (n - r + i);
            ans /= i;
        }
        return ans;
    }

    // Function to return the number of
    // ways to distribute N identical
    // objects in R distinct objects
    static int NoOfDistributions(int N, int R)
    {
        return ncr(N - 1, R - 1);
    }

    // Driver code
    static public void Main ()
    {
        int N = 4;
        int R = 3;

        Console.WriteLine(NoOfDistributions(N, R));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to return the
// value of ncr effectively
function ncr(n, r)
{

    // Initialize the answer
    let ans = 1;

    for(let i = 1; i <= r; i += 1)
    {

        // Divide simultaneously by
        // i to avoid overflow
        ans *= (n - r + i);
        ans = parseInt(ans / i);
    }
    return ans;
}

// Function to return the number of
// ways to distribute N identical
// objects in R distinct objects
function NoOfDistributions(N, R)
{
    return ncr(N - 1, R - 1);
}

// Driver code
let N = 4;
let R = 3;

document.write(NoOfDistributions(N, R));

// This code is contributed by rishavmahato348

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(R)