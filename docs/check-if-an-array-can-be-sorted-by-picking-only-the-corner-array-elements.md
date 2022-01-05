# 检查一个数组是否可以通过只拾取角数组元素来排序

> 原文:[https://www . geesforgeks . org/check-if-a-array-can-sort-by-picking-only-the-corner-array-elements/](https://www.geeksforgeeks.org/check-if-an-array-can-be-sorted-by-picking-only-the-corner-array-elements/)

给定一个由 **N** 元素组成的数组**arr【】**，任务是检查给定的数组是否可以通过只选取角元素来排序，即可以选择数组左侧或右侧的元素。

**示例:**

> **输入:** arr[] = {2，3，4，10，4，3，1}
> **输出:**是
> **解释:**
> 从数组中拾取元素并放置在排序数组中的顺序如下:
> {2，3，4，10，4，3，**1**}->{ 1 }
> {**2**，3，4，10 2，3}
> {4，10，4， **3** } - > {1，2，3，3}
> { **4** ，10，4} - > {1，2，3，3，4}
> {10， **4** } - > {1，2，3，3，4，4}
> {10} - > {1

**方法:**要解决这个问题，我们需要使用一个类似于[双音素序列](https://www.geeksforgeeks.org/find-bitonic-point-given-bitonic-sequence/)的概念。按照以下步骤解决问题:

*   遍历数组并检查数组元素的顺序是否在减少，即如果下一个元素小于前一个元素，那么所有剩余的元素也应该减少或相等。
*   也就是说，如果顺序是**非递增**、**非递减**或**非递减后非递增**，那么只有这样数组才能按照给定的操作排序。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if an array can
// be sorted using given operations
bool check(int arr[], int n)
{
    int i, g;
    g = 0;
    for (i = 1; i < n; i++) {

        // If sequence becomes increasing
        // after an already non-decreasing to
        // non-increasing pattern
        if (arr[i] - arr[i - 1] > 0 && g == 1)
            return false;

        // If a decreasing pattern is observed
        if (arr[i] - arr[i - 1] < 0)
            g = 1;
    }
    return true;
}

// Driver Code
int main()
{

    int arr[] = { 2, 3, 4, 10, 4, 3, 1 };
    int n = sizeof(arr) / sizeof(int);
    if (check(arr, n) == true)
        cout << "Yes"
                "\n";
    else
        cout << "No"
             << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Function to check if an array can
// be sorted using given operations
static boolean check(int arr[], int n)
{
    int i, g;
    g = 0;

    for(i = 1; i < n; i++)
    {

        // If sequence becomes increasing
        // after an already non-decreasing to
        // non-increasing pattern
        if (arr[i] - arr[i - 1] > 0 && g == 1)
            return false;

        // If a decreasing pattern is observed
        if (arr[i] - arr[i - 1] < 0)
            g = 1;
    }
    return true;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 2, 3, 4, 10, 4, 3, 1 };
    int n = arr.length;

    if (check(arr, n) == true)
    {
        System.out.println("Yes");
    } else
    {
        System.out.println("No");
    }
}
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check if an array can
# be sorted using given operations
def check(arr, n):

    g = 0

    for i in range(1, n):

        # If sequence becomes increasing
        # after an already non-decreasing to
        # non-increasing pattern
        if(arr[i] - arr[i - 1] > 0 and g == 1):
            return False

        # If a decreasing pattern is observed
        if(arr[i] - arr[i] < 0):
            g = 1

    return True

# Driver Code
arr = [ 2, 3, 4, 10, 4, 3, 1 ]
n = len(arr)

if(check(arr, n) == True):
    print("Yes")
else:
    print("No")

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to check if an array can
// be sorted using given operations
static bool check(int []arr, int n)
{
    int i, g;
    g = 0;

    for(i = 1; i < n; i++)
    {

        // If sequence becomes increasing
        // after an already non-decreasing to
        // non-increasing pattern
        if (arr[i] - arr[i - 1] > 0 && g == 1)
            return false;

        // If a decreasing pattern is observed
        if (arr[i] - arr[i - 1] < 0)
            g = 1;
    }
    return true;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 2, 3, 4, 10, 4, 3, 1 };
    int n = arr.Length;

    if (check(arr, n) == true)
    {
        Console.WriteLine("Yes");
    } else
    {
        Console.WriteLine("No");
    }
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>
// Javascript Program to implement
// the above approach

// Function to check if an array can
// be sorted using given operations
function check(arr, n)
{
    var i, g;
    g = 0;
    for (i = 1; i < n; i++) {

        // If sequence becomes increasing
        // after an already non-decreasing to
        // non-increasing pattern
        if (arr[i] - arr[i - 1] > 0 && g == 1)
            return false;

        // If a decreasing pattern is observed
        if (arr[i] - arr[i - 1] < 0)
            g = 1;
    }
    return true;
}

// Driver Code
var arr = [ 2, 3, 4, 10, 4, 3, 1 ];
var n = arr.length;
if (check(arr, n) == true)
    document.write( "Yes"+
            "<br>");
else
    document.write( "No"
         + "<br>");

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*