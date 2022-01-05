# 仅使用数组元素计算目标数的方法数量

> 原文:[https://www . geeksforgeeks . org/仅使用数组元素计算目标数的方法数/](https://www.geeksforgeeks.org/number-of-ways-to-calculate-a-target-number-using-only-array-elements/)

给定一个整数数组，找到仅使用数组元素和加法或减法运算符计算目标数的多种方法。

**示例:**

```
Input: arr[] = {-3, 1, 3, 5}, k = 6
Output: 4
Explanation - 
- (-3) + (3)
+ (1) + (5)
+ (-3) + (1) + (3) + (5)
- (-3) + (1) - (3) + (5)

Input: arr[] = {2, 3, -4, 4}, k = 5
Output: 6
Explanation - 
+ (2) + (3)
+ (2) + (3) + (4) + (-4)
+ (2) + (3) - (4) - (-4)
- (3) + (4) - (-4)
- (2) + (3) + (4)
- (2) + (3) - (-4)
```

这个问题类似于 [0-1 背包问题](https://www.geeksforgeeks.org/dynamic-programming-set-10-0-1-knapsack-problem/)，对于每个物品，我们要么挑选完整的物品，要么根本不挑选(0-1 属性)。这里的想法保持不变，即我们要么包含当前数字，要么忽略它。如果我们包括当前数字，我们从剩余目标中减去或加上它，并用新目标递归剩余数字。如果目标达到 0，我们就增加计数。如果我们已经处理了数组的所有元素，但没有达到目标，计数保持不变。

下面是上述思想的递归实现。

## C++

```
// C++ program to find the number of ways to calculate
// a target number using only array elements and
// addition or subtraction operator.
#include <iostream>
#include <vector>
using namespace std;

// Function to find the number of ways to calculate
// a target number using only array elements and
// addition or subtraction operator.
int findTotalWays(vector<int> arr, int i, int k)
{

    // If target is reached, return 1
    if (k == 0 && i == arr.size())
        return 1;

    // If all elements are processed and
    // target is not reached, return 0
    if (i >= arr.size())
        return 0;

    // Return total count of three cases
    // 1\. Don't consider current element
    // 2\. Consider current element and subtract it from target
    // 3\. Consider current element and add it to target
    return findTotalWays(arr, i + 1, k)
           + findTotalWays(arr, i + 1, k - arr[i])
           + findTotalWays(arr, i + 1, k + arr[i]);
}

// Driver Program
int main()
{
    vector<int> arr = { -3, 1, 3, 5, 7 };

    // target number
    int k = 6;

    cout << findTotalWays(arr, 0, k) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number
// of ways to calculate a target
// number using only array elements and
// addition or subtraction operator.
import java.util.*;

class GFG {

    // Function to find the number of ways to calculate
    // a target number using only array elements and
    // addition or subtraction operator.
    static int findTotalWays(Vector<Integer> arr, int i, int k)
    {

        // If target is reached, return 1
        if (k == 0 && i == arr.size()) {
            return 1;
        }

        // If all elements are processed and
        // target is not reached, return 0
        if (i >= arr.size()) {
            return 0;
        }

        // Return total count of three cases
        // 1\. Don't consider current element
        // 2\. Consider current element and subtract it from target
        // 3\. Consider current element and add it to target
        return findTotalWays(arr, i + 1, k)
            + findTotalWays(arr, i + 1, k - arr.get(i))
            + findTotalWays(arr, i + 1, k + arr.get(i));
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] arr = { -3, 1, 3, 5 };
        Vector<Integer> v = new Vector<Integer>();
        for (int a : arr) {
            v.add(a);
        }

        // target number
        int k = 6;

        System.out.println(findTotalWays(v, 0, k));
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 program to find the number of
# ways to calculate a target number using
# only array elements and addition or
# subtraction operator.

# Function to find the number of ways to
# calculate a target number using only
# array elements and addition or
# subtraction operator.
def findTotalWays(arr, i, k):

    # If target is reached, return 1
    if (k == 0 and i == len(arr)):
        return 1   

    # If all elements are processed and
    # target is not reached, return 0
    if (i >= len(arr)):
        return 0

    # Return total count of three cases
    # 1\. Don't consider current element
    # 2\. Consider current element and
    # subtract it from target
    # 3\. Consider current element and
    # add it to target
    return (findTotalWays(arr, i + 1, k) +
            findTotalWays(arr, i + 1, k - arr[i]) +
            findTotalWays(arr, i + 1, k + arr[i]))

# Driver Code
if __name__ == '__main__':
    arr = [-3, 1, 3, 5, 7]

    # target number
    k = 6

    print(findTotalWays(arr, 0, k))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find the number
// of ways to calculate a target
// number using only array elements and
// addition or subtraction operator.
using System;
using System.Collections.Generic;

class GFG {

    // Function to find the number of ways to calculate
    // a target number using only array elements and
    // addition or subtraction operator.
    static int findTotalWays(List<int> arr, int i, int k)
    {
        // If target is reached, return 1
        if (k == 0 && i ==  arr.Count) {
            return 1;
        }

        // If all elements are processed and
        // target is not reached, return 0
        if (i >= arr.Count) {
            return 0;
        }

        // Return total count of three cases
        // 1\. Don't consider current element
        // 2\. Consider current element and subtract it from target
        // 3\. Consider current element and add it to target
        return findTotalWays(arr, i + 1, k)
            + findTotalWays(arr, i + 1, k - arr[i])
            + findTotalWays(arr, i + 1, k + arr[i]);
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] arr = { -3, 1, 3, 5, 7 };
        List<int> v = new List<int>();
        foreach(int a in arr)
        {
            v.Add(a);
        }

        // target number
        int k = 6;

        Console.WriteLine(findTotalWays(v, 0, k));
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to find the number
// of ways to calculate a target
// number using only array elements and
// addition or subtraction operator.

// Function to find the number of ways to
// calculate a target number using only
// array elements and addition or
// subtraction operator.
function findTotalWays(arr, i, k)
{

    // If target is reached, return 1
    if (k == 0 && i == arr.length)
    {
        return 1;
    }

    // If all elements are processed and
    // target is not reached, return 0
    if (i >= arr.length)
    {
        return 0;
    }

    // Return total count of three cases
    // 1\. Don't consider current element
    // 2\. Consider current element and
    //    subtract it from target
    // 3\. Consider current element and
    //    add it to target
    return findTotalWays(arr, i + 1, k) +
           findTotalWays(arr, i + 1, k - arr[i]) +
           findTotalWays(arr, i + 1, k + arr[i]);
}

// Driver code
let arr = [ -3, 1, 3, 5 ,7 ];
let k = 6;

document.write(findTotalWays(arr, 0, k));

// This code is contributed by rag2127

</script>
```

**输出:**

```
10
```

**时间复杂度:**o(3^n)
T3】辅助空间: O(n)

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如发现任何不正确的地方，请写评论，或者您想分享更多关于上述话题的信息