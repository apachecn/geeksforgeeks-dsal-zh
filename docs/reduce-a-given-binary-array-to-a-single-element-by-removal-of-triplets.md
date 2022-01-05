# 通过移除三元组将给定的二进制数组简化为单个元素

> 原文:[https://www . geesforgeks . org/通过移除三元组将给定的二进制数组减少为单个元素/](https://www.geeksforgeeks.org/reduce-a-given-binary-array-to-a-single-element-by-removal-of-triplets/)

给定二进制数组 **arr[]** cof 大小 **N** ，任务是通过以下两个操作将数组简化为单个元素:

*   连续三个 **0** 或 **1** 保持不变。
*   由**两个 0 和一个 1 组成的连续数组元素的三元组(反之亦然)**可以转换为更频繁的元素。

**示例:**

> **输入:** arr[] = {0，1，1，1，0，0，1，1，1，1，1，1}
> **输出:**否
> **解释:**
> 以下是对数组执行的操作:
> {0，1，1} - > 1 将数组修改为{1，1，1，0，0，1，1}
> {1，0，0} - > 0 修改
> 因此，数组不能简化为单个元素。
> 
> **输入:** arr[] = {1，0，0，0，1，1}
> **输出:**是
> **解释:**
> 以下是对数组执行的操作:
> {1，0，0} - > 0 {0，0，1，1，1}
> {0，0，1} - > 0 {0，1，1}
> {0，1，1} - >

**方法:**
按照以下步骤解决问题:

*   计算 **0** 和 **1** 的频率。
*   计算它们各自计数的绝对差值。
*   如果差值为 1，则只有这样数组才能缩减为 1。因此，打印“是”。
*   否则，打印否。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if it is possible to
// reduce the array to a single element
void solve(int arr[], int n)
{
    // Stores frequency of 0's
    int countzeroes = 0;

    // Stores frequency of 1's
    int countones = 0;

    for (int i = 0; i < n; i++) {

        if (arr[i] == 0)
            countzeroes++;
        else
            countones++;
    }

    // Condition for array to be reduced
    if (abs(countzeroes - countones) == 1)
        cout << "Yes";

    // Otherwise
    else
        cout << "No";
}

// Driver Code
int main()
{
    int arr[] = { 0, 1, 0, 0, 1, 1, 1 };

    int n = sizeof(arr) / sizeof(arr[0]);

    solve(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Function to check if it is possible to
// reduce the array to a single element
static void solve(int arr[], int n)
{

    // Stores frequency of 0's
    int countzeroes = 0;

    // Stores frequency of 1's
    int countones = 0;

    for(int i = 0; i < n; i++)
    {
        if (arr[i] == 0)
            countzeroes++;
        else
            countones++;
    }

    // Condition for array to be reduced
    if (Math.abs(countzeroes - countones) == 1)
        System.out.print("Yes");

    // Otherwise
    else
        System.out.print("No");
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 0, 1, 0, 0, 1, 1, 1 };

    int n = arr.length;

    solve(arr, n);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check if it is possible to
# reduce the array to a single element
def solve(arr, n):

    # Stores frequency of 0's
    countzeroes = 0;

    # Stores frequency of 1's
    countones = 0;

    for i in range(n):
        if (arr[i] == 0):
            countzeroes += 1;
        else:
            countones += 1;

    # Condition for array to be reduced
    if (abs(countzeroes - countones) == 1):
        print("Yes");

    # Otherwise
    else:
        print("No");

# Driver Code
if __name__ == '__main__':

    arr = [ 0, 1, 0, 0, 1, 1, 1 ];

    n = len(arr);

    solve(arr, n);

# This code is contributed by Amit Katiyar
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to check if it is possible to
// reduce the array to a single element
static void solve(int []arr, int n)
{

    // Stores frequency of 0's
    int countzeroes = 0;

    // Stores frequency of 1's
    int countones = 0;

    for(int i = 0; i < n; i++)
    {
        if (arr[i] == 0)
            countzeroes++;
        else
            countones++;
    }

    // Condition for array to be reduced
    if (Math.Abs(countzeroes - countones) == 1)
        Console.Write("Yes");

    // Otherwise
    else
        Console.Write("No");
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 0, 1, 0, 0, 1, 1, 1 };

    int n = arr.Length;

    solve(arr, n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to check if it is possible to
// reduce the array to a single element
function solve(arr, n)
{

    // Stores frequency of 0's
    var countzeroes = 0;

    // Stores frequency of 1's
    var countones = 0;

    for(var i = 0; i < n; i++)
    {
        if (arr[i] == 0)
            countzeroes++;
        else
            countones++;
    }

    // Condition for array to be reduced
    if (Math.abs(countzeroes - countones) == 1)
        document.write( "Yes");

    // Otherwise
    else
        document.write( "No");
}

// Driver Code
var arr = [ 0, 1, 0, 0, 1, 1, 1 ];
var n = arr.length;

solve(arr, n);

// This code is contributed by rutvik_56

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*