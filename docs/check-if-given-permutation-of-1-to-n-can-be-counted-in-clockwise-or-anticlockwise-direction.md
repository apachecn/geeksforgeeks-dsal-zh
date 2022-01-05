# 检查给定的 1 到 N 的排列是否可以顺时针或逆时针计数

> 原文:[https://www . geesforgeks . org/check-if-给定-排列-1 到-n-可按顺时针或逆时针方向计数/](https://www.geeksforgeeks.org/check-if-given-permutation-of-1-to-n-can-be-counted-in-clockwise-or-anticlockwise-direction/)

给定一个大小为 **N** 的整数数组 **arr** ，其中包含从 **1** 到 **N** 的不同元素。任务是检查是否可以找到数组中的一个位置，使得从 **1** 到 **N** 的所有数字都可以顺时针或逆时针计数。
**示例:**

```
Input: arr[] = [2, 3, 4, 5, 1]
Output: YES
Explanation:
                    1   2 
                  5       3
                      4
If counting is start at index 4
then all numbers can be counted
from 1 to N in a clockwise order.

Input: arr[] = {1, 2, 3, 5, 4]
Output: NO
Explanation: 
There is no any index in array
from which given array can count
1 to N in clockwise order or
counterclockwise order.
```

**进场:**以上问题可以通过观察分析解决。

1.  只有当连续元素之间的绝对差大于 **1** 的计数正好是 **1** 时，才能找到数组中的索引，因为只有这样才有可能按照顺时针或逆时针的顺序从 **1** 计数到 **N** 。
2.  如果相邻元素之间的绝对差的计数大于 **1** ，则无法按顺时针或逆时针顺序从 **1** 计数到 **N** 。

下面是上述方法的基本实现:

## C++

```
// C++ program to check Clockwise or
// counterclockwise order in an array

#include <bits/stdc++.h>
using namespace std;

bool check_order(vector<int> arr)
{
    int cnt = 0;
    for (int i = 0; i < arr.size() - 1; i++) {
        if (abs(arr[i + 1] - arr[i]) > 1)
            cnt++;
    }
    // Comparing the first and last
    // value of array
    if (abs(arr[0] - arr[arr.size() - 1]) > 1)
        cnt++;

    // If the Count is greater
    // than 1 then it can't be
    // represented in required order
    if (cnt > 1)
        return false;
    return true;
}

// Driver function
int main()
{
    vector<int> arr = { 2, 3, 4, 5, 1 };
    if (check_order(arr))
        cout << "YES";
    else
        cout << "NO";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check clockwise or
// counterclockwise order in an array
class GFG{

static boolean check_order(int []arr)
{
    int cnt = 0;
    for(int i = 0; i < arr.length - 1; i++)
    {
        if (Math.abs(arr[i + 1] -
                     arr[i]) > 1)
            cnt++;
    }

    // Comparing the first and last
    // value of array
    if (Math.abs(arr[0] -
                 arr[arr.length - 1]) > 1)
        cnt++;

    // If the Count is greater
    // than 1 then it can't be
    // represented in required order
    if (cnt > 1)
        return false;

    return true;
}

// Driver code
public static void main(String[] args)
{
    int []arr = { 2, 3, 4, 5, 1 };

    if (check_order(arr))
        System.out.print("YES");
    else
        System.out.print("NO");
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to check clockwise or
# counterclockwise order in an array
def check_order(arr):

    cnt = 0
    for i in range(len(arr) - 1):
        if (abs(arr[i + 1] - arr[i]) > 1):
            cnt += 1

    # Comparing the first and last
    # value of array
    if (abs(arr[0] - arr[len(arr) - 1]) > 1):
        cnt += 1

    # If the count is greater
    # than 1 then it can't be
    # represented in required order
    if (cnt > 1):
        return False

    return True

# Driver code
arr = [ 2, 3, 4, 5, 1 ]

if (check_order(arr)):
    print("YES")
else:
    print("NO")

# This code is contributed by Vishal Maurya.
```

## C#

```
// C# program to check clockwise or
// counterclockwise order in an array
using System;

class GFG{

static bool check_order(int []arr)
{
    int cnt = 0;

    for(int i = 0; i < arr.Length - 1; i++)
    {
        if (Math.Abs(arr[i + 1] -
                   arr[i]) > 1)
            cnt++;
    }

    // Comparing the first and last
    // value of array
    if (Math.Abs(arr[0] -
                 arr[arr.Length - 1]) > 1)
        cnt++;

    // If the Count is greater
    // than 1 then it can't be
    // represented in required order
    if (cnt > 1)
        return false;

    return true;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 2, 3, 4, 5, 1 };

    if (check_order(arr))
        Console.Write("YES");
    else
        Console.Write("NO");
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program to check clockwise or
// counterclockwise order in an array   
function check_order(arr)
{
        var cnt = 0;
        for (i = 0; i < arr.length - 1; i++)
        {
            if (Math.abs(arr[i + 1] - arr[i]) > 1)
                cnt++;
        }

        // Comparing the first and last
        // value of array
        if (Math.abs(arr[0] - arr[arr.length - 1]) > 1)
            cnt++;

        // If the Count is greater
        // than 1 then it can't be
        // represented in required order
        if (cnt > 1)
            return false;

        return true;
    }

    // Driver code

        var arr = [ 2, 3, 4, 5, 1 ];

        if (check_order(arr))
            document.write("YES");
        else
            document.write("NO");

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
YES
```

***时间复杂度:** O (N)*
***辅助空间:** O (1)*