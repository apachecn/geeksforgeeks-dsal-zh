# 检查是否可以通过允许的相邻条件交换对数组进行排序

> 原文:[https://www . geesforgeks . org/check-可能-排序-数组-条件-交换-相邻-允许/](https://www.geeksforgeeks.org/check-possible-sort-array-conditional-swapping-adjacent-allowed/)

我们得到了一个从 0 到 n-1 的整数数组。我们可以多次交换数组中的相邻元素，但前提是这些元素之间的绝对差值为 1。检查是否可以对数组进行排序。如果是，则打印“是”或“否”。
示例:

```
Input : arr[] = {1, 0, 3, 2}
Output : yes
Explanation:- We can swap arr[0] and arr[1].
Again we swap arr[2] and arr[3]. 
Final arr[] = {0, 1, 2, 3}.

Input : arr[] = {2, 1, 0}
Output : no
```

虽然这些问题乍一看很复杂，但有一个简单的解决方案。如果我们从左到右遍历数组，并确保在到达 I 之前对索引 I 之前的元素进行排序，那么我们必须具有最大 arr[0..这个最大值必须小于 arr[i]或者只比 arr[i]大一个。在第一种情况下，我们只是继续前进。在第二种情况下，我们交换并继续前进。
将当前元素与数组中的下一个元素进行比较。如果当前元素大于下一个元素，则执行以下操作:-
…a)检查两个数字之间的差值是否为 1，然后交换它。
…b)否则返回假。
到达阵尾，返回真。

## C++

```
// C++ program to check if we can sort
// an array with adjacent swaps allowed
#include<bits/stdc++.h>
using namespace std;

// Returns true if it is possible to sort
// else false/
bool checkForSorting(int arr[], int n)
{
    for (int i=0; i<n-1; i++)
    {
        // We need to do something only if
        // previousl element is greater
        if (arr[i] > arr[i+1])
        {
            if (arr[i] - arr[i+1] == 1)
                swap(arr[i], arr[i+1]);

            // If difference is more than
            // one, then not possible
            else
                return false;
        }
    }
    return true;
}

// Driver code
int main()
{
    int arr[] = {1,0,3,2};
    int n = sizeof(arr)/sizeof(arr[0]);
    if (checkForSorting(arr, n))
       cout << "Yes";
    else
       cout << "No";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class Main
{
    // Returns true if it is possible to sort
    // else false/
    static boolean checkForSorting(int arr[], int n)
    {
        for (int i=0; i<n-1; i++)
        {
            // We need to do something only if
            // previousl element is greater
            if (arr[i] > arr[i+1])
            {
                if (arr[i] - arr[i+1] == 1)
                    {
                        // swapping
                        int temp = arr[i];
                        arr[i] = arr[i+1];
                        arr[i+1] = temp;
                    }

                // If difference is more than
                // one, then not possible
                else
                    return false;
            }
        }
        return true;
    }

    // Driver function
    public static void main(String args[])
    {
        int arr[] = {1,0,3,2};
        int n = arr.length;
        if (checkForSorting(arr, n))
           System.out.println("Yes");
        else
           System.out.println("No");
    }
}
```

## 蟒蛇 3

```
# Python 3 program to
# check if we can sort
# an array with adjacent
# swaps allowed

# Returns true if it
# is possible to sort
# else false/
def checkForSorting(arr, n):

    for i in range(0,n-1):

        # We need to do something only if
        # previousl element is greater
        if (arr[i] > arr[i+1]):

            if (arr[i] - arr[i+1] == 1):
                arr[i], arr[i+1] = arr[i+1], arr[i]

            # If difference is more than
            # one, then not possible
            else:
                return False

    return True

# Driver code
arr = [1,0,3,2]
n = len(arr)
if (checkForSorting(arr, n)):
    print("Yes")
else:
    print("No")

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# program to check if we can sort
// an array with adjacent swaps allowed
using System;

class GFG
{
    // Returns true if it is
    // possible to sort else false
    static bool checkForSorting(int []arr, int n)
    {
        for (int i=0; i<n-1; i++)
        {
            // We need to do something only if
            // previousl element is greater
            if (arr[i] > arr[i+1])
            {
                if (arr[i] - arr[i+1] == 1)
                    {
                        // swapping
                        int temp = arr[i];
                        arr[i] = arr[i+1];
                        arr[i+1] = temp;
                    }

                // If difference is more than
                // one, then not possible
                else
                    return false;
            }
        }
        return true;
    }

    // Driver function
    public static void Main()
    {
        int []arr = {1, 0, 3, 2};
        int n = arr.Length;
        if (checkForSorting(arr, n))
        Console.Write("Yes");
        else
        Console.Write("No");
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if we can sort
// an array with adjacent swaps allowed
// Returns true if it is possible to sort
// else false

function checkForSorting($arr, $n)
{
    $temp = 0;
    for ($i = 0; $i < $n - 1; $i++)
    {

        // We need to do something only if
        // previousl element is greater
        if ($arr[$i] > $arr[$i + 1])
        {
            if ($arr[$i] - $arr[$i + 1] == 1)
                {
                        // swapping
                        $temp = $arr[$i];
                        $arr[$i] = $arr[$i + 1];
                        $arr[$i + 1] = $temp;
                }

            // If difference is more than
            // one, then not possible
            else
                return false;
        }
    }
    return true;
}

    // Driver Code
    $arr = array(1,0,3,2);
    $n = sizeof($arr);
    if (checkForSorting($arr, $n))
        echo "Yes";
    else
        echo "No";

// This code is contributed
// by nitin mittal.
?>
```

## java 描述语言

```
<script>

// JavaScript program to check if we can sort
// an array with adjacent swaps allowed
// Returns true if it is possible to sort
// else false

function checkForSorting(arr, n)
{
    let temp = 0;
    for (let i = 0; i < n - 1; i++)
    {

        // We need to do something only if
        // previousl element is greater
        if (arr[i] > arr[i + 1])
        {
            if (arr[i] - arr[i + 1] == 1)
                {
                        // swapping
                        temp = arr[i];
                        arr[i] = arr[i + 1];
                        arr[i + 1] = temp;
                }

            // If difference is more than
            // one, then not possible
            else
                return false;
        }
    }
    return true;
}

    // Driver Code
    let arr = new Array(1,0,3,2);
    let n = arr.length;
    if (checkForSorting(arr, n))
        document.write("Yes");
    else
        document.write("No");

// This code is contributed
// by nitin gfgking

</script>
```

**输出:**

```
Yes
```

**时间复杂度** =O(n)

**辅助空间** =O(1)
本文由 **Roshni Agarwal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。