# 选择一个整数 K，使得 K 与所有数组元素的异或值的最大值最小

> 原文:[https://www . geeksforgeeks . org/choose-a-integer-k-so-将所有数组元素的 k 的最大异或值最小化/](https://www.geeksforgeeks.org/choose-an-integer-k-such-that-maximum-of-the-xor-values-of-k-with-all-array-elements-is-minimized/)

给定一个由非负整数 **N** 组成的数组 **A** ，任务是选择一个整数 **K** ，使得 K 与所有数组元素的异或值的最大值最小。换句话说，找到 Z 的最小可能值，其中 **Z = max(A[i] xor K)** ，0 < = i < = n-1，对于 K 的某个值。
**示例:**

> **输入:**A =【1，2，3】
> **输出:** 2
> **说明:**
> 在选择 K = 3 时，max(A[i] xor 3) = 2，这是最小可能值。
> **输入:** A = [3，2，5，6]
> **输出:** 5

**方法:**为了解决上面提到的问题，我们将使用[递归](https://www.geeksforgeeks.org/recursion/)。我们将从递归函数中的最高有效位开始。

*   在递归步骤中，将元素分成两部分，一部分当前位为开，另一部分当前位为关。如果任何部分没有一个元素，那么可以选择 K 的这个特定位，使得最终的 xor 值在这个位位置为 0(因为我们的目标是最小化这个值)，然后在下一个递归步骤中前进到下一个位。

*   如果这两个部分都有一些元素，那么通过将 0 和 1 放在这个位位置并在下一次递归调用中使用相应的部分计算答案来探索这两种可能性。如果在该位置(位置)放置 1，则让**答案 _ 开**为值，如果放置 0，则让**答案 _ 关**为值。由于两个部分都不是空的，无论我们为 K 选择哪个位，2 <sup>位置</sup>将被添加到最终值中。
    对于每个递归步骤:

> 答案= min(答案 _on，答案 _ off)+2<sup>pos</sup>T2】

以下是上述方法的实现:

## C++

```
// C++ implementation to find Minimum
// possible value of the maximum xor
// in an array by choosing some integer

#include <bits/stdc++.h>
using namespace std;

// Function to calculate Minimum possible
// value of the Maximum XOR in an array
int calculate(vector<int>& section, int pos)
{
    // base case
    if (pos < 0)
        return 0;

    // Divide elements into two sections
    vector<int> on_section, off_section;

    // Traverse all elements of current
    // section and divide in two groups
    for (auto el : section) {
        if (((el >> pos) & 1) == 0)
            off_section.push_back(el);

        else
            on_section.push_back(el);
    }

    // Check if one of the sections is empty
    if (off_section.size() == 0)
        return calculate(on_section, pos - 1);

    if (on_section.size() == 0)
        return calculate(off_section, pos - 1);

    // explore both the possibilities using recursion
    return min(calculate(off_section, pos - 1),
               calculate(on_section, pos - 1))
           + (1 << pos);
}

// Function to calculate minimum XOR value
int minXorValue(int a[], int n)
{
    vector<int> section;
    for (int i = 0; i < n; i++)
        section.push_back(a[i]);

    // Start recursion from the
    // most significant pos position
    return calculate(section, 30);
}

// Driver code
int main()
{
    int N = 4;

    int A[N] = { 3, 2, 5, 6 };

    cout << minXorValue(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find Minimum
// possible value of the maximum xor
// in an array by choosing some integer
import java.util.*;

class GFG{

// Function to calculate Minimum possible
// value of the Maximum XOR in an array
static int calculate(Vector<Integer> section, int pos)
{

    // Base case
    if (pos < 0)
        return 0;

    // Divide elements into two sections
    Vector<Integer> on_section = new Vector<Integer>(),
                   off_section = new Vector<Integer>();

    // Traverse all elements of current
    // section and divide in two groups
    for(int el : section)
    {
       if (((el >> pos) & 1) == 0)
           off_section.add(el);
       else
           on_section.add(el);
    }

    // Check if one of the sections is empty
    if (off_section.size() == 0)
        return calculate(on_section, pos - 1);

    if (on_section.size() == 0)
        return calculate(off_section, pos - 1);

    // Explore both the possibilities using recursion
    return Math.min(calculate(off_section, pos - 1),
                    calculate(on_section, pos - 1)) +
                             (1 << pos);
}

// Function to calculate minimum XOR value
static int minXorValue(int a[], int n)
{
    Vector<Integer> section = new Vector<Integer>();

    for(int i = 0; i < n; i++)
       section.add(a[i]);

    // Start recursion from the
    // most significant pos position
    return calculate(section, 30);
}

// Driver code
public static void main(String[] args)
{
    int N = 4;
    int A[] = { 3, 2, 5, 6 };

    System.out.print(minXorValue(A, N));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation to find Minimum
# possible value of the maximum xor
# in an array by choosing some integer

# Function to calculate Minimum possible
# value of the Maximum XOR in an array

def calculate(section, pos):

    # base case
    if (pos < 0):
        return 0

    # Divide elements into two sections
    on_section = []
    off_section = []

    # Traverse all elements of current
    # section and divide in two groups
    for el in section:
        if (((el >> pos) & 1) == 0):
            off_section.append(el)

        else:
            on_section.append(el)

    # Check if one of the sections is empty
    if (len(off_section) == 0):
        return calculate(on_section, pos - 1)

    if (len(on_section) == 0):
        return calculate(off_section, pos - 1)

    # explore both the possibilities using recursion
    return min(calculate(off_section, pos - 1),
               calculate(on_section, pos - 1))+ (1 << pos)

# Function to calculate minimum XOR value
def minXorValue(a, n):
    section = []
    for i in range( n):
        section.append(a[i]);

    # Start recursion from the
    # most significant pos position
    return calculate(section, 30)

# Driver code
if __name__ == "__main__":
    N = 4

    A = [ 3, 2, 5, 6 ]

    print(minXorValue(A, N))

# This code is contributed by chitranayal   
```

## C#

```
// C# implementation to find minimum
// possible value of the maximum xor
// in an array by choosing some integer
using System;
using System.Collections.Generic;

class GFG{

// Function to calculate minimum possible
// value of the maximum XOR in an array
static int calculate(List<int> section, int pos)
{

    // Base case
    if (pos < 0)
        return 0;

    // Divide elements into two sections
    List<int> on_section = new List<int>(),
             off_section = new List<int>();

    // Traverse all elements of current
    // section and divide in two groups
    foreach(int el in section)
    {
        if (((el >> pos) & 1) == 0)
            off_section.Add(el);
        else
            on_section.Add(el);
    }

    // Check if one of the sections is empty
    if (off_section.Count == 0)
        return calculate(on_section, pos - 1);

    if (on_section.Count == 0)
        return calculate(off_section, pos - 1);

    // Explore both the possibilities using recursion
    return Math.Min(calculate(off_section, pos - 1),
                    calculate(on_section, pos - 1)) +
                             (1 << pos);
}

// Function to calculate minimum XOR value
static int minXorValue(int []a, int n)
{
    List<int> section = new List<int>();

    for(int i = 0; i < n; i++)
       section.Add(a[i]);

    // Start recursion from the
    // most significant pos position
    return calculate(section, 30);
}

// Driver code
public static void Main(String[] args)
{
    int N = 4;
    int []A = { 3, 2, 5, 6 };

    Console.Write(minXorValue(A, N));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript implementation to find Minimum
// possible value of the maximum xor
// in an array by choosing some integer

// Function to calculate Minimum possible
// value of the Maximum XOR in an array
function calculate(section, pos)
{
    // base case
    if (pos < 0)
        return 0;

    // Divide elements into two sections
    let on_section = [], off_section = [];

    // Traverse all elements of current
    // section and divide in two groups
    for (let el = 0; el < section.length; el++) {
        if (((section[el] >> pos) & 1) == 0)
            off_section.push(section[el]);

        else
            on_section.push(section[el]);
    }

    // Check if one of the sections is empty
    if (off_section.length == 0)
        return calculate(on_section, pos - 1);

    if (on_section.length == 0)
        return calculate(off_section, pos - 1);

    // explore both the possibilities using recursion
    return Math.min(calculate(off_section, pos - 1),
               calculate(on_section, pos - 1))
           + (1 << pos);
}

// Function to calculate minimum XOR value
function minXorValue(a, n)
{
    let section = [];
    for (let i = 0; i < n; i++)
        section.push(a[i]);

    // Start recursion from the
    // most significant pos position
    return calculate(section, 30);
}

// Driver code
    let N = 4;

    let A = [ 3, 2, 5, 6 ];

    document.write(minXorValue(A, N));

</script>
```

**Output:** 

```
5
```

**时间复杂度:***O(N * log(max(A<sub>I</sub>)*