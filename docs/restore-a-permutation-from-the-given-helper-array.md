# 从给定的辅助数组中恢复排列

> 原文:[https://www . geeksforgeeks . org/restore-a-置换-从给定的辅助数组/](https://www.geeksforgeeks.org/restore-a-permutation-from-the-given-helper-array/)

给定一个大小为**N–1**的数组 **Q[]** ，使得每个**Q[I]= P[I+1]–P[I]**，其中 **P[]** 是第一个 **N** 自然数的排列，任务是找到这个排列。如果找不到有效的排列 **P[]** ，则打印 **-1** 。

**示例:**

> **输入:** Q[] = {-2，1 }
> T3】输出: 3 1 2
> 
> **输入:** Q[] = {1，1，1，1}
> **输出:** 1 2 3 4 5

**进场:**这是一道数学算法题。让我们表示 **P[i] = x** 。因此**P[I+1]= P[I]+(P[I+1]–P[I])= x+Q[I]**(因为**Q[I]= P[I+1]–P[I]**)。
因此，**P[I+2]= P[I]+(P[I+1]–P[I])+(P[I+2]–P[I+1])= x+Q[I]+Q[I+1]**。观察这里形成的图案。 **P** 无非是 **[x，x + Q[1]，x+Q[1]+Q[2]+…+x+Q[1]+Q[2]+…+Q[n–1]]**其中 **x = P[i]** 这还是未知数。
我们来排列一下 **P'** 其中**P '[I]= P[I]–x**。因此， **P' = [0，Q[1]，Q[1] + Q[2]，Q[1] + Q[2] + Q[3]，…，Q[1]+Q[2]+…+Q[n–1]]**。

要找到 **x** ，让我们找到**P’**中最小的元素。顺其自然**P【k】**。因此，**x = 1–P '[k]**。这是因为，原排列 **P** 有从 **1** 到 **n** 的整数，所以 **1** 可以是 **P** 中的最小元素。找到 **x** 后，在每个**P‘**上加上 **x** ，得到原始排列 **P** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the required permutation
void findPerm(int Q[], int n)
{

    int minval = 0, qsum = 0;
    for (int i = 0; i < n - 1; i++) {

        // Each element in P' is like a
        // cumulative sum in Q
        qsum += Q[i];

        // minval is the minimum
        // value in P'
        if (qsum < minval)
            minval = qsum;
    }
    vector<int> P(n);
    P[0] = 1 - minval;

    // To check if each entry in P
    // is from the range [1, n]
    bool permFound = true;
    for (int i = 0; i < n - 1; i++) {
        P[i + 1] = P[i] + Q[i];

        // Invalid permutation
        if (P[i + 1] > n || P[i + 1] < 1) {
            permFound = false;
            break;
        }
    }

    // If a valid permutation exists
    if (permFound) {

        // Print the permutation
        for (int i = 0; i < n; i++) {
            cout << P[i] << " ";
        }
    }
    else {

        // No valid permutation
        cout << -1;
    }
}

// Driver code
int main()
{
    int Q[] = { -2, 1 };
    int n = 1 + (sizeof(Q) / sizeof(int));

    findPerm(Q, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

// Function to find the required permutation
static void findPerm(int Q[], int n)
{

    int minval = 0, qsum = 0;
    for (int i = 0; i < n - 1; i++)
    {

        // Each element in P' is like a
        // cumulative sum in Q
        qsum += Q[i];

        // minval is the minimum
        // value in P'
        if (qsum < minval)
            minval = qsum;
    }
    int []P = new int[n];
    P[0] = 1 - minval;

    // To check if each entry in P
    // is from the range [1, n]
    boolean permFound = true;
    for (int i = 0; i < n - 1; i++)
    {
        P[i + 1] = P[i] + Q[i];

        // Invalid permutation
        if (P[i + 1] > n || P[i + 1] < 1)
        {
            permFound = false;
            break;
        }
    }

    // If a valid permutation exists
    if (permFound)
    {

        // Print the permutation
        for (int i = 0; i < n; i++)
        {
            System.out.print(P[i]+ " ");
        }
    }
    else
    {

        // No valid permutation
        System.out.print(-1);
    }
}

// Driver code
public static void main(String[] args)
{
    int Q[] = { -2, 1 };
    int n = 1 + Q.length;

    findPerm(Q, n);

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find the required permutation
def findPerm(Q, n) :

    minval = 0; qsum = 0;
    for i in range(n - 1) :

        # Each element in P' is like a
        # cumulative sum in Q
        qsum += Q[i];

        # minval is the minimum
        # value in P'
        if (qsum < minval) :
            minval = qsum;

    P = [0]*n;
    P[0] = 1 - minval;

    # To check if each entry in P
    # is from the range [1, n]
    permFound = True;

    for i in range(n - 1) :
        P[i + 1] = P[i] + Q[i];

        # Invalid permutation
        if (P[i + 1] > n or P[i + 1] < 1) :
            permFound = False;
            break;

    # If a valid permutation exists
    if (permFound) :

        # Print the permutation
        for i in range(n) :
            print(P[i],end=" ");
    else :

        # No valid permutation
        print(-1);

# Driver code
if __name__ == "__main__" :

    Q = [ -2, 1 ];
    n = 1 + len(Q) ;

    findPerm(Q, n);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to find the required permutation
static void findPerm(int []Q, int n)
{

    int minval = 0, qsum = 0;
    for (int i = 0; i < n - 1; i++)
    {

        // Each element in P' is like a
        // cumulative sum in Q
        qsum += Q[i];

        // minval is the minimum
        // value in P'
        if (qsum < minval)
            minval = qsum;
    }
    int []P = new int[n];
    P[0] = 1 - minval;

    // To check if each entry in P
    // is from the range [1, n]
    bool permFound = true;
    for (int i = 0; i < n - 1; i++)
    {
        P[i + 1] = P[i] + Q[i];

        // Invalid permutation
        if (P[i + 1] > n || P[i + 1] < 1)
        {
            permFound = false;
            break;
        }
    }

    // If a valid permutation exists
    if (permFound)
    {

        // Print the permutation
        for (int i = 0; i < n; i++)
        {
            Console.Write(P[i]+ " ");
        }
    }
    else
    {

        // No valid permutation
        Console.Write(-1);
    }
}

// Driver code
public static void Main(String[] args)
{
    int []Q = { -2, 1 };
    int n = 1 + Q.Length;

    findPerm(Q, n);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to find the required permutation
function findPerm(Q, n)
{
    var minval = 0, qsum = 0;
    for(var i = 0; i < n - 1; i++)
    {

        // Each element in P' is like a
        // cumulative sum in Q
        qsum += Q[i];

        // minval is the minimum
        // value in P'
        if (qsum < minval)
            minval = qsum;
    }
    var P = Array(n);
    P[0] = 1 - minval;

    // To check if each entry in P
    // is from the range [1, n]
    var permFound = true;
    for(var i = 0; i < n - 1; i++)
    {
        P[i + 1] = P[i] + Q[i];

        // Invalid permutation
        if (P[i + 1] > n || P[i + 1] < 1)
        {
            permFound = false;
            break;
        }
    }

    // If a valid permutation exists
    if (permFound)
    {

        // Print the permutation
        for(var i = 0; i < n; i++)
        {
            document.write( P[i] + " ");
        }
    }
    else
    {

        // No valid permutation
        document.write( -1);
    }
}

// Driver code
var Q = [ -2, 1 ];
var n = 1 + Q.length;

findPerm(Q, n);

// This code is contributed by famously

</script>
```

**Output:** 

```
3 1 2
```