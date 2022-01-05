# 通过交换由另一个数组指定的不同类型的元素来排序一个数组

> 原文:[https://www . geeksforgeeks . org/通过交换由另一个数组指定的不同类型的元素来排序数组/](https://www.geeksforgeeks.org/sort-an-array-by-swapping-elements-of-different-type-specified-by-another-array/)

给定两个分别包含整数元素及其各自类型(类型 0 或类型 1)的**数组 a[]和 b[]** ，任务是检查是否有可能仅通过交换不同类型的元素以非递减顺序对数组进行排序。
**例:**

> **输入:** a[] = {30，20，20，10}，b[] = {1，1，1，1}
> **输出:**否
> **解释:**
> 由于所有元素都是同一类型，因此不允许交换，并且给定数组没有按非递减顺序排序。
> **输入:** a[] = {6，5，4}，b[] = {1，1，0}
> **输出:**是
> **说明:**
> 交换 4 和 6 将数组转换为非递减顺序。

**方法:**
要解决上述问题，需要进行以下观察:

*   如果数组 **a【】已经按照非递减顺序排序**，那么答案是**是**。
*   如果数组 **a【】没有排序**并且所有元素都是同一类型，那么答案是**否**，因为不可能交换。
*   在任何其他情况下，答案都是**是**，因为我们总是可以对数组进行排序。这是因为我们将至少有一个元素的类型不同于其他元素，因此我们可以将其与所有其他元素交换任意多次，直到所有元素都处于它们的排序位置。

以下是上述方法的实现:

## C++

```
// C++ program to check if it
// is possible to sort the
// array in non-decreasing
// order by swapping
// elements of different types

#include <bits/stdc++.h>
using namespace std;

// Function to check if it is
// possible to sort the array
// in non-decreasing order by
// swapping elements of
// different types
bool sorting_possible(int a[],
                      int b[], int n)
{
    // Consider the array
    // to be already sorted
    bool sorted = true;

    int type1 = 0, type0 = 0, i;

    // checking if array is
    // already sorted
    for (i = 1; i < n; i++) {
        // Check for a pair which
        // is in decreasing order
        if (a[i] < a[i - 1]) {

            sorted = false;
            break;
        }
    }

    // Count the frequency of
    // each type of element
    for (i = 0; i < n; i++) {
        // type0 stores count
        // of elements of type 0
        if (b[i] == 0)
            type0++;

        // type1 stores count
        // of elements of type 1
        else
            type1++;
    }

    // Return true if array
    // is already sorted
    if (sorted)
        return true;

    // Return false if all
    // elements are of same
    // type and array
    // is unsorted
    else if (type1 == n
             || type0 == n)
        return false;

    // Possible for all
    // other cases
    else
        return true;
}

// Driver Program
int main()
{
    int a[] = { 15, 1, 2, 17, 6 };
    int b[] = { 1, 1, 0, 1, 1 };
    int n = sizeof(a) / sizeof(a[0]);

    bool res = sorting_possible(a, b, n);

    if (res)
        cout << "Yes";
    else
        cout << "No";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if it is
// possible to sort the array in
// non-decreasing order by swapping
// elements of different types
import java.util.*;

class GFG{

// Function to check if it is
// possible to sort the array
// in non-decreasing order by
// swapping elements of
// different types
static boolean sorting_possible(int a[],
                                int b[],
                                int n)
{

    // Consider the array
    // to be already sorted
    boolean sorted = true;

    int type1 = 0, type0 = 0, i;

    // Checking if array is
    // already sorted
    for(i = 1; i < n; i++)
    {

       // Check for a pair which
       // is in decreasing order
       if (a[i] < a[i - 1])
       {
           sorted = false;
           break;
       }
    }

    // Count the frequency of
    // each type of element
    for(i = 0; i < n; i++)
    {

       // type0 stores count
       // of elements of type 0
       if (b[i] == 0)
           type0++;

       // type1 stores count
       // of elements of type 1
       else
           type1++;
    }

    // Return true if array
    // is already sorted
    if (sorted)
        return true;

    // Return false if all elements
    // are of same type and array
    // is unsorted
    else if (type1 == n || type0 == n)
        return false;

    // Possible for all
    // other cases
    else
        return true;
}

// Driver code
public static void main(String[] args)
{
    int a[] = { 15, 1, 2, 17, 6 };
    int b[] = { 1, 1, 0, 1, 1 };
    int n = a.length;

    boolean res = sorting_possible(a, b, n);

    if (res)
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to check if it
# is possible to sort the
# array in non-decreasing
# order by swapping
# elements of different types

# Function to check if it is
# possible to sort the array
# in non-decreasing order by
# swapping elements of different types
def sorting_possible(a, b, n):

    # Consider the array
    # to be already sorted
    sorted = True

    type1 = 0
    type0 = 0

    # Checking if array is
    # already sorted
    for i in range(1, n):

        # Check for a pair which
        # is in decreasing order
        if (a[i] < a[i - 1]):
            sorted = False
            break

    # Count the frequency of
    # each type of element
    for i in range(n):

        # type0 stores count
        # of elements of type 0
        if (b[i] == 0):
            type0 += 1

        # type1 stores count
        # of elements of type 1
        else:
            type1 += 1

    # Return true if array
    # is already sorted
    if (sorted != False):
        return True

    # Return false if all elements
    # are of same type and array
    # is unsorted
    elif (type1 == n or type0 == n):
        return False

    # Possible for all
    # other cases
    else:
        return True

# Driver code
a = [ 15, 1, 2, 17, 6 ]
b = [ 1, 1, 0, 1, 1 ]

n = len(a)
res = sorting_possible(a, b, n)

if (res != False):
    print("Yes")
else:
    print("No")

# This code is contributed by sanjoy_62
```

## C#

```
// C# program to check if it is
// possible to sort the array in
// non-decreasing order by swapping
// elements of different types
using System;

class GFG{

// Function to check if it is
// possible to sort the array
// in non-decreasing order by
// swapping elements of
// different types
static bool sorting_possible(int []a,
                             int []b,
                             int n)
{

    // Consider the array
    // to be already sorted
    bool sorted = true;

    int type1 = 0, type0 = 0, i;

    // Checking if array is
    // already sorted
    for(i = 1; i < n; i++)
    {

       // Check for a pair which
       // is in decreasing order
       if (a[i] < a[i - 1])
       {
           sorted = false;
           break;
       }
    }

    // Count the frequency of
    // each type of element
    for(i = 0; i < n; i++)
    {

       // type0 stores count
       // of elements of type 0
       if (b[i] == 0)
           type0++;

       // type1 stores count
       // of elements of type 1
       else
           type1++;
    }

    // Return true if array
    // is already sorted
    if (sorted)
        return true;

    // Return false if all elements
    // are of same type and array
    // is unsorted
    else if (type1 == n || type0 == n)
        return false;

    // Possible for all
    // other cases
    else
        return true;
}

// Driver code
public static void Main(String[] args)
{
    int []a = { 15, 1, 2, 17, 6 };
    int []b = { 1, 1, 0, 1, 1 };
    int n = a.Length;

    bool res = sorting_possible(a, b, n);

    if (res)
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to check if it is
// possible to sort the array in
// non-decreasing order by swapping
// elements of different types

// Function to check if it is
// possible to sort the array
// in non-decreasing order by
// swapping elements of
// different types
function sorting_possible(a,b, n)
{

    // Consider the array
    // to be already sorted
    let sorted = true;

    let type1 = 0, type0 = 0, i;

    // Checking if array is
    // already sorted
    for(i = 1; i < n; i++)
    {

       // Check for a pair which
       // is in decreasing order
       if (a[i] < a[i - 1])
       {
           sorted = false;
           break;
       }
    }

    // Count the frequency of
    // each type of element
    for(i = 0; i < n; i++)
    {

       // type0 stores count
       // of elements of type 0
       if (b[i] == 0)
           type0++;

       // type1 stores count
       // of elements of type 1
       else
           type1++;
    }

    // Return true if array
    // is already sorted
    if (sorted)
        return true;

    // Return false if all elements
    // are of same type and array
    // is unsorted
    else if (type1 == n || type0 == n)
        return false;

    // Possible for all
    // other cases
    else
        return true;
}

// Driver code
    let a = [ 15, 1, 2, 17, 6 ];
    let b = [ 1, 1, 0, 1, 1 ];
    let n = a.length;

    let res = sorting_possible(a, b, n);

    if (res)
        document.write("Yes");
    else
        document.write("No");

// This code is contributed by souravghosh0416.
</script>
```

**Output:** 

```
Yes
```

**插图:**

> a[] = {15，1，2，17，6}
> 只有 2 为 0 型，其余为 1 型。
> 因此以下步骤导致排序的数组:
> 15，1， **2** ，17，**6**–>15，1， **6** ，17， **2**
> 15，1，6， **17，2** - > 15，1，6， **2，17**
> **15，**