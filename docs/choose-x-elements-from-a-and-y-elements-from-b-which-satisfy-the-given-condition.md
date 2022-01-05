# 从 A[]中选择 X 元素，从 B[]中选择满足给定条件的 Y 元素

> 原文:[https://www . geesforgeks . org/choose-x-elements-from-a-和-y-elements-from-b-满足给定条件/](https://www.geeksforgeeks.org/choose-x-elements-from-a-and-y-elements-from-b-which-satisfy-the-given-condition/)

给定两个数组 **A[]** 和 **B[]** 以及两个整数 **X** 和 **Y** ，任务是从 **A[]** 和 **Y** 元素中选择 **X** 元素，使得从 **B[]** 中选择的所有元素少于从**B[**
T21 中选择的所有元素

> **输入:** A[] = {1，1，1，1，1}，B[] = {3，1}，X = 3，Y = 1
> **输出:**是
> 从 A[]中选择{1，1，1}，从 B[]中选择{3}。
> **输入:** A[] = {5，4}，B[] = {2，3，2，2}，X = 2，Y = 1
> **输出:**否

**方法:**为了满足给定的条件，最小的 **X** 元素必须从**A【】**中选择，最大的 **Y** 元素必须从**B【】**中选择。这可以通过对两个数组进行排序，然后从 **A[]** 中选择 **X <sup>th</sup>** 最小的元素，说 **xSmall** 和**Y<sup>th</sup>T21 从 **B[]** 中选择**最大的元素来完成。
这是因为如果 **xSmall** 小于 **yLarge** ，那么所有小于它的元素肯定会小于 **yLarge** ，所有大于 **yLarge** 的元素肯定会大于 **xSmall** 。
以下是上述方法的实施:**** 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to that returns true if
// it possible to choose the elements
bool isPossible(int A[], int B[], int n,
                int m, int x, int y)
{

    // If elements can't be chosen
    if (x > n || y > m)
        return false;

    // Sort both the arrays
    sort(A, A + n);
    sort(B, B + m);

    // If xth smallest element of A[]
    // is smaller than the yth
    // greatest element of B[]
    if (A[x - 1] < B[m - y])
        return true;
    else
        return false;
}

// Driver code
int main()
{
    int A[] = { 1, 1, 1, 1, 1 };
    int B[] = { 2, 2 };
    int n = sizeof(A) / sizeof(int);
    int m = sizeof(B) / sizeof(int);
    int x = 3, y = 1;

    if (isPossible(A, B, n, m, x, y))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG
{

    // Function to that returns true if
    // it possible to choose the elements
    static boolean isPossible(int A[], int B[], int n,
                              int m, int x, int y)
    {

        // If elements can't be chosen
        if (x > n || y > m)
            return false;

        // Sort both the arrays
        Arrays.sort(A);
        Arrays.sort(B);

        // If xth smallest element of A[]
        // is smaller than the yth
        // greatest element of B[]
        if (A[x - 1] < B[m - y])
            return true;
        else
            return false;
    }

    // Driver code
    public static void main (String[] args)
    {
        int A[] = { 1, 1, 1, 1, 1 };
        int B[] = { 2, 2 };
        int n = A.length;
        int m = B.length;;
        int x = 3, y = 1;

        if (isPossible(A, B, n, m, x, y))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to that returns true if
# it possible to choose the elements
def isPossible(A, B, n, m, x, y) :

    # If elements can't be chosen
    if (x > n or y > m) :
        return False

    # Sort both the arrays
    A.sort()
    B.sort()

    # If xth smallest element of A[]
    # is smaller than the yth
    # greatest element of B[]
    if (A[x - 1] < B[m - y]) :
        return True
    else :
        return False

# Driver code
A = [ 1, 1, 1, 1, 1 ]
B = [ 2, 2 ]
n = len(A)
m = len(B)
x = 3
y = 1

if (isPossible(A, B, n, m, x, y)):
    print("Yes")
else:
    print("No")

# This code is contributed by
# divyamohan123
```

## C#

```
// C# implementation of the above approach
using System;        

class GFG
{

    // Function to that returns true if
    // it possible to choose the elements
    static bool isPossible(int []A, int []B, int n,
                           int m, int x, int y)
    {

        // If elements can't be chosen
        if (x > n || y > m)
            return false;

        // Sort both the arrays
        Array.Sort(A);
        Array.Sort(B);

        // If xth smallest element of A[]
        // is smaller than the yth
        // greatest element of B[]
        if (A[x - 1] < B[m - y])
            return true;
        else
            return false;
    }

    // Driver code
    public static void Main (String[] args)
    {
        int []A = { 1, 1, 1, 1, 1 };
        int []B = { 2, 2 };
        int n = A.Length;
        int m = B.Length;;
        int x = 3, y = 1;

        if (isPossible(A, B, n, m, x, y))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// javascript implementation of the above approach

// Function to that returns true if
// it possible to choose the elements
function isPossible(A , B , n, m , x , y)
{

    // If elements can't be chosen
    if (x > n || y > m)
        return false;

    // Sort both the arrays
    A.sort();
    B.sort();

    // If xth smallest element of A
    // is smaller than the yth
    // greatest element of B
    if (A[x - 1] < B[m - y])
        return true;
    else
        return false;
}

// Driver code

var A = [ 1, 1, 1, 1, 1 ];
var B = [ 2, 2 ];
var n = A.length;
var m = B.length;;
var x = 3, y = 1;

if (isPossible(A, B, n, m, x, y))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by 29AjayKumar

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(N*log(N))

**辅助空间:** O(1)