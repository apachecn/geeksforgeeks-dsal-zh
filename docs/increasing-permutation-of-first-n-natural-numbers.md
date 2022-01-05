# 增加前 N 个自然数的排列

> 原文:[https://www . geeksforgeeks . org/递增排列第一个 n 个自然数/](https://www.geeksforgeeks.org/increasing-permutation-of-first-n-natural-numbers/)

给定一个排列 **{P <sub>1</sub> ，P <sub>2</sub> ，P <sub>3</sub> ，…..P <sub>N</sub> )** 第一个 **N** 自然数。任务是检查是否有可能通过交换任意两个数字来增加排列。如果已经是递增顺序，就什么都不做。
**示例:**

> **输入:** a[] = {5，2，3，4，1}
> **输出:**是
> 交换 1 和 5
> **输入:** a[] = {1，2，3，4，5}
> **输出:**是
> 已按递增顺序
> **输入:** a[] = {5，2，1，4，3}
> **输出:【T18**

**方法:**让 **K** 为 **i** 的位置数，在该位置上**P<sub>1</sub>I**(基于 1 的索引)。如果 **K = 0** ，答案是**是**，因为排列可以保持原样。**如果 K = 2** ，答案也是**是**:调换两个错位的元素。(注意 **K = 1** 是永远不可能的，好像任何元素被放在错误的位置，原本应该在那个位置的元素也一定放错了位置。).如果 **K > 2** 那么答案是**否**:单次互换只能影响两个元素，因此最多只能纠正两次错位。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if it is
// possible to make the permutation
// increasing by swapping any two numbers
bool isPossible(int a[], int n)
{
    // To count misplaced elements
    int k = 0;

    // Count all misplaced elements
    for (int i = 0; i < n; i++) {
        if (a[i] != i + 1)
            k++;
    }

    // If possible
    if (k <= 2)
        return true;

    return false;
}

// Driver code
int main()
{
    int a[] = { 5, 2, 3, 4, 1 };
    int n = sizeof(a) / sizeof(a[0]);

    if (isPossible(a, n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function that returns true if it is
// possible to make the permutation
// increasing by swapping any two numbers
static boolean isPossible(int a[], int n)
{
    // To count misplaced elements
    int k = 0;

    // Count all misplaced elements
    for (int i = 0; i < n; i++)
    {
        if (a[i] != i + 1)
            k++;
    }

    // If possible
    if (k <= 2)
        return true;

    return false;
}

// Driver code
public static void main(String[] args)
{
    int a[] = { 5, 2, 3, 4, 1 };
    int n = a.length;

    if (isPossible(a, n))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by Code_Mech
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if it is
# possible to make the permutation
# increasing by swapping any two numbers
def isPossible(a, n) :

    # To count misplaced elements
    k = 0;

    # Count all misplaced elements
    for i in range(n) :
        if (a[i] != i + 1) :
            k += 1;

    # If possible
    if (k <= 2) :
        return True;

    return False;

# Driver code
if __name__ == "__main__" :

    a = [5, 2, 3, 4, 1 ];
    n = len(a);

    if (isPossible(a, n)) :
        print("Yes");
    else :
        print("No");

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function that returns true if it is
// possible to make the permutation
// increasing by swapping any two numbers
static Boolean isPossible(int []a, int n)
{
    // To count misplaced elements
    int k = 0;

    // Count all misplaced elements
    for (int i = 0; i < n; i++)
    {
        if (a[i] != i + 1)
            k++;
    }

    // If possible
    if (k <= 2)
        return true;

    return false;
}

// Driver code
public static void Main(String[] args)
{
    int []a = { 5, 2, 3, 4, 1 };
    int n = a.Length;

    if (isPossible(a, n))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns true if it is
// possible to make the permutation
// increasing by swapping any two numbers
function isPossible(a, n)
{

    // To count misplaced elements
    let k = 0;

    // Count all misplaced elements
    for (let i = 0; i < n; i++) {
        if (a[i] != i + 1)
            k++;
    }

    // If possible
    if (k <= 2)
        return true;

    return false;
}

// Driver code
    let a = [ 5, 2, 3, 4, 1 ];
    let n = a.length;

    if (isPossible(a, n))
        document.write("Yes");
    else
        document.write("No");

// This code is contributed by Manoj
</script>
```

**Output:** 

```
Yes
```