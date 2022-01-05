# 从给定的三个数组中找出三个元素，使它们的和为 X |集合 2

> 原文:[https://www . geeksforgeeks . org/find-从给定的三个数组中找到三个元素-这样它们的和就是-x-set-2/](https://www.geeksforgeeks.org/find-three-element-from-given-three-arrays-such-that-their-sum-is-x-set-2/)

给定三个排序的整数数组 **A[]** 、 **B[]** 和 **C[]** ，任务是找到三个整数，每个数组一个，这样它们相加得到一个给定的目标值 **X** 。打印**是**还是**否**取决于这种三元组是否存在。
**示例:**

> **输入:** A[] = {2}，B[] = {1，6，7}，C[] = {4，5}，X = 12
> **输出:**是
> A[0]+B[1]+C[0]= 2+6+4 = 12
> **输入:** A[] = {2}，B[] = {1，6，7}，C[] = {4，5}，X = 14
> **输出**

**方法:**我们已经在这篇[文章](https://www.geeksforgeeks.org/find-three-element-from-different-three-arrays-such-that-that-a-b-c-k/)中讨论了一种基于散列的方法，它占用了 O(N)个额外空间。
在本文中，我们将使用占用 O(1)个额外空间的空间高效方法来解决这个问题。这个想法是使用双指针技术。
我们将遍历所有数组中最小的一个，对于每个索引 **i** ，我们将在较大的两个数组上使用双指针来找到一个和等于**X–A[I]**的对(假设 **A[]** 是三个数组中长度最小的一个)。
现在，在较大的两个数组上使用两个指针背后的想法是什么？我们将试着从一个例子中理解同样的事情。

> 让我们假设
> len(A)= 100000
> len(B)= 10000
> len(C)= 10
> **情况 1:** 在较大的两个数组上应用两个指针
> 迭代次数的顺序为= len(C)*(len(A)+len(B))= 10 *(110000)= 110000
> **情况 2:** 在较小的两个数组上应用两个指针【T10 = 1001000000
> **情况 3:** 在最小和最大的数组上应用两个指针
> 迭代次数的顺序将是= len(B)*(len(A)+len(C))= 10000 *(100000+10)= 100010000
> 正如我们所看到的，**情况 1** 对于这个例子来说是最优的，并且很容易证明它一般是最优的

**算法:**

1.  按照数组长度的递增顺序对数组进行排序。
2.  假设排序后的最小数组是 A[]。然后，遍历 A[]的所有元素，对于每个索引“I”，在另外两个数组上应用双指针。我们将在数组 B[]的开头放置一个指针，在数组 C[]的结尾放置一个指针。让我们分别称指针为“j”和“k”。
    *   如果 B[j]+C[k]= X–A[I]，我们找到了匹配。
    *   如果 B[j] + C[k]小于 X–A[I]，我们将“j”的值增加 1。
    *   如果 B[j] + C[k]大于 X–A[I]，我们将“k”的值减少 1。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if there
// exists a triplet with sum x
bool existsTriplet(int a[], int b[],
                   int c[], int x, int l1,
                   int l2, int l3)
{
    // Sorting arrays such that a[]
    // represents smallest array
    if (l2 <= l1 and l2 <= l3)
        swap(l2, l1), swap(a, b);
    else if (l3 <= l1 and l3 <= l2)
        swap(l3, l1), swap(a, c);

    // Iterating the smallest array
    for (int i = 0; i < l1; i++) {

        // Two pointers on second and third array
        int j = 0, k = l3 - 1;
        while (j < l2 and k >= 0) {

            // If a valid triplet is found
            if (a[i] + b[j] + c[k] == x)
                return true;
            if (a[i] + b[j] + c[k] < x)
                j++;
            else
                k--;
        }
    }

    return false;
}

// Driver code
int main()
{
    int a[] = { 2, 7, 8, 10, 15 };
    int b[] = { 1, 6, 7, 8 };
    int c[] = { 4, 5, 5 };
    int l1 = sizeof(a) / sizeof(int);
    int l2 = sizeof(b) / sizeof(int);
    int l3 = sizeof(c) / sizeof(int);

    int x = 14;

    if (existsTriplet(a, b, c, x, l1, l2, l3))
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

// Function that returns true if there
// exists a triplet with sum x
static boolean existsTriplet(int a[], int b[],
                      int c[], int x, int l1,
                              int l2, int l3)
{
    // Sorting arrays such that a[]
    // represents smallest array
    if (l2 <= l1 && l2 <= l3)
    {
        swap(l2, l1);
        swap(a, b);
    }
    else if (l3 <= l1 && l3 <= l2)
    {
        swap(l3, l1);
        swap(a, c);
    }

    // Iterating the smallest array
    for (int i = 0; i < l1; i++)
    {

        // Two pointers on second and third array
        int j = 0, k = l3 - 1;
        while (j < l2 && k >= 0)
        {

            // If a valid triplet is found
            if (a[i] + b[j] + c[k] == x)
                return true;
            if (a[i] + b[j] + c[k] < x)
                j++;
            else
                k--;
        }
    }
    return false;
}

private static void swap(int x, int y)
{
    int temp = x;
    x = y;
    y = temp;
}

private static void swap(int []x, int []y)
{
    int []temp = x;
    x = y;
    y = temp;
}

// Driver code
public static void main(String[] args)
{
    int a[] = { 2, 7, 8, 10, 15 };
    int b[] = { 1, 6, 7, 8 };
    int c[] = { 4, 5, 5 };
    int l1 = a.length;
    int l2 = b.length;
    int l3 = c.length;

    int x = 14;

    if (existsTriplet(a, b, c, x, l1, l2, l3))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Function that returns True if there
# exists a triplet with sum x
def existsTriplet(a, b,c, x, l1,l2, l3):

    # Sorting arrays such that a
    # represents smallest array
    if (l2 <= l1 and l2 <= l3):
        l1, l2 = l2,l1
        a, b = b,a
    elif (l3 <= l1 and l3 <= l2):
        l1, l3 = l3,l1
        a, c = c,a

    # Iterating the smallest array
    for i in range(l1):

        # Two pointers on second and third array
        j = 0
        k = l3 - 1
        while (j < l2 and k >= 0):

            # If a valid triplet is found
            if (a[i] + b[j] + c[k] == x):
                return True
            if (a[i] + b[j] + c[k] < x):
                j += 1
            else:
                k -= 1

    return False

# Driver code
a = [ 2, 7, 8, 10, 15 ]
b = [ 1, 6, 7, 8 ]
c = [ 4, 5, 5 ]
l1 = len(a)
l2 = len(b)
l3 = len(c)

x = 14

if (existsTriplet(a, b, c, x, l1, l2, l3)):
    print("Yes")
else:
    print("No")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function that returns true if there
// exists a triplet with sum x
static bool existsTriplet(int []a, int []b,
                          int []c, int x, int l1,
                          int l2, int l3)
{
    // Sorting arrays such that a[]
    // represents smallest array
    if (l2 <= l1 && l2 <= l3)
    {
        swap(l2, l1);
        swap(a, b);
    }
    else if (l3 <= l1 && l3 <= l2)
    {
        swap(l3, l1);
        swap(a, c);
    }

    // Iterating the smallest array
    for (int i = 0; i < l1; i++)
    {

        // Two pointers on second and third array
        int j = 0, k = l3 - 1;
        while (j < l2 && k >= 0)
        {

            // If a valid triplet is found
            if (a[i] + b[j] + c[k] == x)
                return true;
            if (a[i] + b[j] + c[k] < x)
                j++;
            else
                k--;
        }
    }
    return false;
}

private static void swap(int x, int y)
{
    int temp = x;
    x = y;
    y = temp;
}

private static void swap(int []x, int []y)
{
    int []temp = x;
    x = y;
    y = temp;
}

// Driver code
public static void Main(String[] args)
{
    int []a = { 2, 7, 8, 10, 15 };
    int []b = { 1, 6, 7, 8 };
    int []c = { 4, 5, 5 };
    int l1 = a.Length;
    int l2 = b.Length;
    int l3 = c.Length;

    int x = 14;

    if (existsTriplet(a, b, c, x, l1, l2, l3))
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

// JavaScript implementation of the approach

// Function that returns true if there
// exists a triplet with sum x
function existsTriplet(a, b, c, x, l1,
                    l2, l3)
{
    // Sorting arrays such that a[]
    // represents smallest array
    if (l2 <= l1 && l2 <= l3)
    {
        temp = l1; l1 = l2; l2 = temp;
        temp = a; a = b; b = temp;
    }

    else if (l3 <= l1 && l3 <= l2)
    {
        temp = l1; l1 = l3; l3 = temp;
        temp = a; a = c; c = temp;
    }
    // Iterating the smallest array
    for (var i = 0; i < l1; i++) {

        // Two pointers on second and third array
        var j = 0, k = l3 - 1;
        while (j < l2 && k >= 0) {

            // If a valid triplet is found
            if (a[i] + b[j] + c[k] == x)
                return true;
            if (a[i] + b[j] + c[k] < x)
                j++;
            else
                k--;
        }
    }

    return false;
}

// Driver code
var a = [ 2, 7, 8, 10, 15 ];
var b = [ 1, 6, 7, 8 ];
var c = [ 4, 5, 5 ];
var l1 = a.length;
var l2 = b.length;
var l3 = c.length;
var x = 14;
if (existsTriplet(a, b, c, x, l1, l2, l3))
    document.write("Yes");
else
    document.write("No");

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(min(len(A)、len(B)、len(C)) * max(len(A)、len(B)、len(C)))
T3】辅助空间 : O(1)。