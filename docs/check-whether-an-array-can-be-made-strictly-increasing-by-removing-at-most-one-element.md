# 通过最多移除一个元素来检查一个数组是否可以严格递增

> 原文:[https://www . geesforgeks . org/check-一个数组是否可以通过最多移除一个元素来严格递增/](https://www.geeksforgeeks.org/check-whether-an-array-can-be-made-strictly-increasing-by-removing-at-most-one-element/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是检查给定的[数组是否可以通过最多移除一个元素来严格增加](https://www.geeksforgeeks.org/convert-to-strictly-increasing-integer-array-with-minimum-changes/)。如果可以使数组严格递增，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** arr[] = {1，1，2}
> **输出:**是
> **解释:**移除 1 的出现将数组修改为{1，2}，这是严格递增数组。
> 
> **输入:** arr[] = {2，2，3，4，5，5 }
> T3】输出:否

**方法:**给定问题可以通过[遍历数组**arr【】**T5】并计算满足条件 **arr[i-1] ≥ arr[i]** 的指标来解决。按照以下步骤解决问题:](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)

*   初始化两个变量，比如说**计数**为 **0** 和**索引**为 **-1** ，分别存储需要删除的元素数和被删除元素的索引。
*   在范围**【1，N–1】**内遍历给定数组，如果**arr【I–1】**的值至少为**arr【I】**，则将**计数**的值增加 **1** ，并将**索引**的值更新为 **i** 。
*   如果**计数**的值大于 **1** ，则打印“**否”**，返回**。**
*   否则，检查以下情况:
    *   如果**计数**的值等于 **0** ，则打印**“是”**并返回**。**
    *   如果**索引**等于**(N–1)**或等于 **0** ，则打印**“是”**并返回。
    *   检查移除**索引**处的元素是否使 **arr【索引–1】<arr【索引+1】**，然后打印“**是”**并返回**。**
    *   检查移除**索引–1**处的元素是否会使 **arr【索引–2】<arr【索引】**，其中**索引–2>= 0**，然后打印**“是”**并返回**。**
    *   检查索引< 0, then print **是否为“是”**并返回。
*   完成上述步骤后，如果以上情况都不满足，则打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find if is it possible
// to make the array strictly increasing
// by removing at most one element
bool check(int arr[], int n)
{
    // Stores the count of numbers that
    // are needed to be removed
    int count = 0;

    // Store the index of the element
    // that needs to be removed
    int index = -1;

    // Traverse the range [1, N - 1]
    for (int i = 1; i < n; i++) {

        // If arr[i-1] is greater than
        // or equal to arr[i]
        if (arr[i - 1] >= arr[i]) {

            // Increment the count by 1
            count++;

            // Update index
            index = i;
        }
    }

    // If count is greater than one
    if (count > 1)
        return false;

    // If no element is removed
    if (count == 0)
        return true;

    // If only the last or the
    // first element is removed
    if (index == n - 1 || index == 1)
        return true;

    // If a[index] is removed
    if (arr[index - 1] < arr[index + 1])
        return true;

    // If a[index - 1] is removed
    if (index - 2 >= 0 && arr[index - 2] < arr[index])
        return true;

      // if there is no element to compare
      if(index < 0)
          return true;

    return false;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 5, 3, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);
    if (check(arr, N))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find if is it possible
// to make the array strictly increasing
// by removing at most one element
public static boolean check(int arr[], int n)
{

    // Stores the count of numbers that
    // are needed to be removed
    int count = 0;

    // Store the index of the element
    // that needs to be removed
    int index = -1;

    // Traverse the range [1, N - 1]
    for(int i = 1; i < n; i++) 
    {

        // If arr[i-1] is greater than
        // or equal to arr[i]
        if (arr[i - 1] >= arr[i])
        {

            // Increment the count by 1
            count++;

            // Update index
            index = i;
        }
    }

    // If count is greater than one
    if (count > 1)
        return false;

    // If no element is removed
    if (count == 0)
        return true;

    // If only the last or the
    // first element is removed
    if (index == n - 1 || index == 1)
        return true;

    // If a[index] is removed
    if (arr[index - 1] < arr[index + 1])
        return true;

    // If a[index - 1] is removed
    if (index - 2 >= 0 && arr[index - 2] < arr[index])
        return true;

      // if there is no element to compare
      if(index < 0)
          return true;

    return false;
}

// Driver Code
public static void main(String args[])
{
    int []arr = { 1, 2, 5, 3, 5 };
    int N = arr.length;

    if (check(arr, N))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by SoumikMondal
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find if is it possible
# to make the array strictly increasing
# by removing at most one element
def check(arr, n):

    # Stores the count of numbers that
    # are needed to be removed
    count = 0

    # Store the index of the element
    # that needs to be removed
    index = -1

    # Traverse the range [1, N - 1]
    for i in range(1, n):

        # If arr[i-1] is greater than
        # or equal to arr[i]
        if (arr[i - 1] >= arr[i]):
            # Increment the count by 1
            count += 1

            # Update index
            index = i

    # If count is greater than one
    if (count > 1):
        return False

    # If no element is removed
    if (count == 0):
        return True

    # If only the last or the
    # first element is removed
    if (index == n - 1 or index == 1):
        return True

    # If a[index] is removed
    if (arr[index - 1] < arr[index + 1]):
        return True

    # If a[index - 1] is removed
    if (arr[index - 2] < arr[index]):
        return True

    return False

# Driver Code
if __name__ == '__main__':
    arr = [1, 2, 5, 3, 5]
    N = len(arr)
    if (check(arr, N)):
        print("Yes")
    else:
        print("No")

# This code is contributed by mohitkumar 29.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find if is it possible
// to make the array strictly increasing
// by removing at most one element
public static bool check(int[] arr, int n)
{

    // Stores the count of numbers that
    // are needed to be removed
    int count = 0;

    // Store the index of the element
    // that needs to be removed
    int index = -1;

    // Traverse the range [1, N - 1]
    for(int i = 1; i < n; i++)
    {

        // If arr[i-1] is greater than
        // or equal to arr[i]
        if (arr[i - 1] >= arr[i])
        {

            // Increment the count by 1
            count++;

            // Update index
            index = i;
        }
    }

    // If count is greater than one
    if (count > 1)
        return false;

    // If no element is removed
    if (count == 0)
        return true;

    // If only the last or the
    // first element is removed
    if (index == n - 1 || index == 1)
        return true;

    // If a[index] is removed
    if (arr[index - 1] < arr[index + 1])
        return true;

    // If a[index - 1] is removed
    if (arr[index - 2] < arr[index])
        return true;

    return false;
}

// Driver Code
public static void Main(string[] args)
{
    int[] arr = { 1, 2, 5, 3, 5 };
    int N = arr.Length;

    if (check(arr, N))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find if is it possible
// to make the array strictly increasing
// by removing at most one element
function check(arr , n)
{

    // Stores the count of numbers that
    // are needed to be removed
    var count = 0;

    // Store the index of the element
    // that needs to be removed
    var index = -1;

    // Traverse the range [1, N - 1]
    for(i = 1; i < n; i++) 
    {

        // If arr[i-1] is greater than
        // or equal to arr[i]
        if (arr[i - 1] >= arr[i])
        {

            // Increment the count by 1
            count++;

            // Update index
            index = i;
        }
    }

    // If count is greater than one
    if (count > 1)
        return false;

    // If no element is removed
    if (count == 0)
        return true;

    // If only the last or the
    // first element is removed
    if (index == n - 1 || index == 1)
        return true;

    // If a[index] is removed
    if (arr[index - 1] < arr[index + 1])
        return true;

    // If a[index - 1] is removed
    if (arr[index - 2] < arr[index])
        return true;

    return false;
}

// Driver Code

var arr = [ 1, 2, 5, 3, 5 ];
var N = arr.length;

if (check(arr, N))
    document.write("Yes");
else
    document.write("No");

// This code contributed by shikhasingrajput 

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)