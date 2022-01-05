# 检查数组中的最小元素是否小于或等于每隔一个元素的一半

> 原文:[https://www . geesforgeks . org/check-如果数组中的最小元素小于或等于其他元素的一半/](https://www.geeksforgeeks.org/check-if-minimum-element-in-array-is-less-than-or-equals-half-of-every-other-element/)

给定一个**数组 arr[]** ，任务是检查数组中的最小元素是否小于或等于其他元素的一半。如果是，则打印“是”，否则打印“否”。
***注:**给定数组中的最小数总是唯一的。*

**示例:**

> **输入:** arr = {2，1，4，5}
> **输出:**是
> **解释:**
> 1 是 arr[]数组中的最小元素，2，4，5 除以 2 得到 1，2，2.5，大于或等于最小数。因此，打印“是”。
> 
> **输入:** arr = {2，4，5，3}
> **输出:**否
> **解释:**
> 2 是 arr[]数组中的最小元素，4，5，3 除以 2 得到 2，2.5，1.5，其中整数 3 不返回大于或等于最小数的值(1.5 < 2)。因此，打印“否”。

**方法 1:**
要解决上面提到的问题，我们必须**借助循环找到最小元素**，然后**再次扫描整个数组**，检查两次最小元素是否小于或等于每隔一个元素。但是这个解决方案使用两个循环花费了 O(N)个时间，并且可以在只涉及一次迭代的情况下进一步优化。

**方法 2:**
为了优化上述解，我们可以**在单次迭代中找到最小的以及第二小的元素**本身。然后简单地检查最小元素的两倍是否小于或等于第二小元素。

下面是上述方法的实现:

## C++

```
// C++ implementation to Check if the minimum element in the
// array is greater than or equal to half of every other elements
#include <bits/stdc++.h>
using namespace std;

// Function to Check if the minimum element in the array is
// greater than or equal to half of every other element
void checkMin(int arr[], int len)
{

    // Initialise the variables to store
    // smallest and second smallest
    int smallest = INT_MAX, secondSmallest = INT_MAX;

    for (int i = 0; i < len; i++) {

        // Check if current element is smaller than smallest,
        // the current smallest will become secondSmallest
        // and current element will be the new smallest
        if (arr[i] < smallest) {
            secondSmallest = smallest;
            smallest = arr[i];
        }

        // Check if current element is smaller than
        // secondSmallest simply update the latter
        else if (arr[i] < secondSmallest) {
            secondSmallest = arr[i];
        }
    }

    if (2 * smallest <= secondSmallest)
        cout << "Yes";
    else
        cout << "No";
}

// Driver code
int main()
{
    int arr[] = { 2, 3, 4, 5 };

    int len = sizeof(arr) / sizeof(arr[0]);

    checkMin(arr, len);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check
// if the minimum element in the
// array is greater than or equal
// to half of every other elements
import java.util.*;
class GFG{

// Function to Check if the minimum
// element in the array is greater
// than or equal to half of every
// other elements
static void checkMin(int arr[], int len)
{

    // Initialise the variables to store
    // smallest and second smallest
    int smallest = Integer.MAX_VALUE;
    int secondSmallest = Integer.MAX_VALUE;

    for(int i = 0; i < len; i++)
    {

       // Check if current element is smaller than 
       // smallest, the current smallest will 
       // become secondSmallest and current 
       // element will be the new smallest
       if (arr[i] < smallest)
       {
           secondSmallest = smallest;
           smallest = arr[i];
       }

       // Check if current element is smaller than
       // secondSmallest simply update the latter
       else if (arr[i] < secondSmallest)
       {
           secondSmallest = arr[i];
       }
    }
    if (2 * smallest <= secondSmallest)
        System.out.print("Yes");
    else
        System.out.print("No");
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 2, 3, 4, 5 };
    int len = arr.length;

    checkMin(arr, len);
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 implementation to Check if
# the minimum element in the array
# is greater than or equal to half
# of every other element
import math

# Function to Check if the minimum element
# in the array is greater than or equal to
# half of every other element
def checkMin(arr, n):

    # Initialise the variables to store
    # smallest and second smallest
    smallest = math.inf
    secondSmallest = math.inf

    for i in range(n):

        # Check if current element is
        # smaller than smallest,
        # the current smallest will become
        # secondSmallest and current element
        # will be the new smallest
        if(arr[i] < smallest):
            secondSmallest = smallest
            smallest = arr[i]

        # Check if current element is smaller than
        # secondSmallest simply update the latter
        elif(arr[i] < secondSmallest):
            secondSmallest = arr[i]

    if(2 * smallest <= secondSmallest):
        print("Yes")
    else:
        print("No")

# Driver code
if __name__ == '__main__':
    arr = [ 2, 3, 4, 5 ]

    n = len(arr)

    checkMin(arr, n)

# This code is contributed by Shivam Singh.
```

## C#

```
// C# implementation to check
// if the minimum element in the
// array is greater than or equal
// to half of every other elements
using System;

class GFG{

// Function to Check if the minimum
// element in the array is greater
// than or equal to half of every
// other elements
static void checkMin(int []arr, int len)
{

    // Initialise the variables to store
    // smallest and second smallest
    int smallest = int.MaxValue;
    int secondSmallest = int.MaxValue;

    for(int i = 0; i < len; i++)
    {

       // Check if current element is smaller than
       // smallest, the current smallest will
       // become secondSmallest and current
       // element will be the new smallest
       if (arr[i] < smallest)
       {
           secondSmallest = smallest;
           smallest = arr[i];
       }

       // Check if current element is smaller than
       // secondSmallest simply update the latter
       else if (arr[i] < secondSmallest)
       {
           secondSmallest = arr[i];
       }
    }
    if (2 * smallest <= secondSmallest)
        Console.Write("Yes");
    else
        Console.Write("No");
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 2, 3, 4, 5 };
    int len = arr.Length;

    checkMin(arr, len);
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// Javascript implementation to check 
// if the minimum element in the
// array is greater than or equal
// to half of every other elements

// Function to Check if the minimum
// element in the array is greater
// than or equal to half of every
// other element
function checkMin(arr, len)
{

    // Initialise the variables to store
    // smallest and second smallest
    var smallest = Number.INFINITY,
        secondSmallest = Number.INFINITY;

    for(var i = 0; i < len; i++)
    {

        // Check if current element is
        // smaller than smallest, the
        // current smallest will become
        // secondSmallest and current
        // element will be the new smallest
        if (arr[i] < smallest)
        {
            secondSmallest = smallest;
            smallest = arr[i];
        }

        // Check if current element is smaller than
        // secondSmallest simply update the latter
        else if (arr[i] < secondSmallest)
        {
            secondSmallest = arr[i];
        }
    }

    if (2 * smallest <= secondSmallest)
        document.write("Yes");
    else
        document.write("No");
}

// Driver code
var arr = [ 2, 3, 4, 5 ];
var len = 4;

checkMin(arr, len);

// This code is contributed by akshitsaxenaa09

</script>
```

**Output:** 

```
No
```

**时间复杂度:** O(N)，其中 N 为给定数组的长度。
**辅助空间:** O(N)。