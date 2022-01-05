# 求给定周期函数的最大可能值

> 原文:[https://www . geesforgeks . org/find-给定周期函数的最大可能值/](https://www.geeksforgeeks.org/find-the-maximum-possible-value-for-the-given-periodic-function/)

给定三个数字 **A、B 和 N** ，任务是找到**楼层(A * x/B)–A *楼层(x / b)** 的最大可能值，其中 x 是小于或等于 N 的非负整数。这里楼层(T) =表示不大于实数 T (G.I.F 函数)的最大整数。
**约束条件:** 1 ≤ A ≤ 10 <sup>6</sup> ，1 ≤ B ≤ 10 <sup>12</sup> ，1 ≤ N ≤ 10 <sup>12</sup> 。输入中的所有值都是整数。

> **输入:** A = 5，B = 7，N = 4
> **输出:** 2
> **说明:**
> 取值 x = 3 取最大值。将此值代入等式:
> 地板((5 * 3)/7)–(5 *地板(3 / 7)) =地板(2.1)–0 = 2。
> 
> **输入:** A = 11，B = 10，N = 9
> T3】输出: 9

**天真法:**这个问题的天真法是考虑从 1 到 N 所有可能的数字，计算最大可能值。

**时间复杂度:** O(N)。

**高效途径:**思路是对函数**f(x)= floor(A * x/B)–A * floor(x/B)**进行观察。

*   我们可以观察到给定的函数是周期函数。这可以通过以下事实来证明:

> f(x + B) =楼层(A *(x +B)/B)–A *楼层((x + B)/B)
> = > f(x + B) =楼层((A * x/B)+A)–A *楼层((x /B) + 1)
> 按楼层-功能属性，楼层(x+整数)=整数+楼层(x)。
> = > f(x + B) =楼层(A * x/B)–A *楼层(x / B) = f(x)

*   因此，我们可以得出结论，0 ≤ x ≤ B。然而，如果 x = B，f(x) = 0。所以我们排除它，得到 0 ≤ x ≤ B-1。
*   但是，我们还必须考虑 x ≤ N 的条件，由于 floor(x)是一个单调非减函数，所以我们必须包含两个范围中的最佳值。
*   因此，当**x = min(B–1，N)** 时，得到 f(x)的最大值。

下面是上述方法的实现:

## C++

```
// C++ Program to find the maximum
// possible value for the given function

#include <iostream>
using namespace std;

// Function to return the maximum
// value of f(x)
int floorMax(int A, int B, int N)
{
    int x = min(B - 1, N);

    return (A * x) / B;
}

// Driver code
int main()
{
    int A = 11, B = 10, N = 9;

    cout << floorMax(A, B, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum
// possible value for the given function
class GFG{

// Function to return the maximum
// value of f(x)
public static int floorMax(int A, int B, int N)
{
    int x = Math.min(B - 1, N);

    return (A * x) / B;
}

// Driver Code
public static void main(String[] args)
{
    int A = 11, B = 10, N = 9;

    System.out.println(floorMax(A, B, N));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to find the maximum
# possible value for the given function

# Function to return the maximum
# value of f(x)
def floorMax(A, B, N):

    x = min(B - 1, N)

    return (A * x) // B

# Driver code
A = 11
B = 10
N = 9

print(floorMax(A, B, N))

# This code is contributed by code_hunt
```

## C#

```
// C# program to find the maximum
// possible value for the given function        
using System;
using System.Collections.Generic;

class GFG{        

// Function to return the maximum
// value of f(x)
static int floorMax(int A, int B, int N)
{
    int x = Math.Min(B - 1, N);

    return (A * x) / B;
}    

// Driver Code        
public static void Main (string[] args)
{        
    int A = 11, B = 10, N = 9;

    Console.Write(floorMax(A, B, N));
}        
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript program to find the maximum
// possible value for the given function

// Function to return the maximum
// value of f(x)
function floorMax(A, B, N)
{
    let x = Math.min(B - 1, N);

    return Math.floor((A * x) / B);
}

// Driver Code

   let A = 11, B = 10, N = 9;

   document.write(floorMax(A, B, N));

</script>
```

**Output:** 

```
9
```

***时间复杂度:** O(1)*