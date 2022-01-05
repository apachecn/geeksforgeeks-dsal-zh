# 检查数组中是否存在每对的乘积

> 原文:[https://www . geesforgeks . org/check-product-ever-pair-exists-array/](https://www.geeksforgeeks.org/check-product-every-pair-exists-array/)

给定一个 n 个整数的数组，我们需要检查每对数字 a[i] & a[j]是否存在 a[k]，使得 a[k] = a[i]*a[j]，其中 k 也可以等于 I 或 j。
**例:**

```
Input : arr[] = {0\. 1} 
Output : Yes
Here a[0]*a[1] is equal to a[0]

Input : arr[] = {5, 6}
Output : No
```

如果数组遵循下面提到的所有条件:
**条件 1 :** 数组必须具有小于或等于 1 的除 1、0、-1 之外的元素数，因为如果它具有多于 1 个这样的元素，则数组中不存在乘积等于这两个(或更多)元素中最大值的元素。假设这种元素的数量是 2，它们的值是 5，6，所以数组中没有等于 5*6 = 30 的元素。
**条件 2 :** 如果数组中还有其他数字，比如 x(除了 0、1 和-1 之外)和-1 也存在，那么同样回答为假。因为-1 的存在使得要求 x 和-x 都应该存在，但是这违反了条件 1。
**条件 3 :** 如果数组中有一个以上的“-1”，并且没有人，那么答案也将是否定的，因为两个“-1”的乘积等于 1。
以下是上述条件的执行情况。

## C++

```
// C++ program to find if
// product of every pair
// is present in array.
#include<bits/stdc++.h>
using namespace std;

// Returns true if product
// of every pair in arr[]
// is present in arr[]
bool checkArray(int arr[] , int n)
{
    // variable to store number
    //  of zeroes, ones, minus
    // one and other numbers.
    int zero = 0, one = 0,
        minusone = 0, other=0;
    for (int i = 0; i < n; i++)
    {
        // incrementing the
        // variable values
        if (arr[i] == 0)
            zero++;
        else if (arr[i] == 1)
            one++;
        else if (arr[i] == -1)
            minusone++;
        else
            other++;
    }

    // checking the conditions
    if (other > 1)
        return false;
    else if (other != 0 &&
             minusone != 0)
        return false;
    else if (minusone > 1 &&
             one == 0)
        return false;

    return true;
}

// Driver Code
int main()
{
    int arr[] = {0, 1, 1, 10};
    int n = sizeof(arr) / sizeof(arr[0]);
    if (checkArray(arr, n))
    cout << "Yes";
    else
    cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// if product of every pair
// is present in array.

class GFG
{
    // Returns true if product
    // of every pair in arr[]
    // is present in arr[]
    static boolean checkArray(int arr[] ,
                              int n)
    {
        // variable to store number
        //  of zeroes, ones, minus
        // one and other numbers.
        int zero = 0, one = 0,
            minusone = 0, other=0;
        for (int i = 0; i < n; i++)
        {
            // incrementing the
            // variable values
            if (arr[i] == 0)
                zero++;
            else if (arr[i] == 1)
                one++;
            else if (arr[i] == -1)
                minusone++;
            else
                other++;
        }

        // checking the conditions
        if (other > 1)
            return false;
        else if (other != 0 &&
                 minusone != 0)
            return false;
        else if (minusone > 1 &&
                 one == 0)
            return false;

        return true;
    }

    // Driver Code
    public static void main (String[] args)
    {
        int arr[] = {0, 1, 1, 10};
        int n = arr.length;
        if (checkArray(arr, n))
        System.out.println("Yes");
        else
        System.out.println("No");
    }
}

// This code is contributed by Harsh Agarwal
```

## 蟒蛇 3

```
# Python3 program to find
# if product of every pair
# is present in array.

# Returns True if product
# of every pair in arr[] is
# present in arr[]
def checkArray(arr, n):

    # variable to store number
    # of zeroes, ones, minus
    # one and other numbers.
    zero = 0; one = 0;
    minusone = 0; other = 0
    for i in range(0, n):

        # incrementing the
        # variable values
        if (arr[i] == 0):
            zero += 1
        elif (arr[i] == 1):
            one += 1
        elif (arr[i] == -1):
            minusone += 1
        else:
            other += 1

    # checking the conditions
    if (other > 1):
        return false
    elif (other != 0 and
          minusone != 0):
        return false
    elif (minusone > 1 and
          one == 0):
        return false

    return True

# Driver Code
arr = [0, 1, 1, 10]
n = len(arr)
if (checkArray(arr, n)):
    print("Yes")
else:
    print("No")

# This code is contributed
# by Smitha Dinesh Semwal.
```

## C#

```
// C# program to find if
// product of every pair
// is present in array.
using System;

class GFG
{
    // Returns true if product
    // of every pair in arr[]
    // is present in arr[]
    static Boolean checkArray(int []arr ,
                              int n)
    {
        // variable to store number
        // of zeroes, ones, minus
        // one and other numbers.
        int zero = 0, one = 0,
            minusone = 0, other=0;
        for (int i = 0; i < n; i++)
        {
            // incrementing the
            // variable values
            if (arr[i] == 0)
                zero++;
            else if (arr[i] == 1)
                one++;
            else if (arr[i] == -1)
                minusone++;
            else
                other++;
        }

        // checking the conditions
        if (other > 1)
            return false;
        else if (other != 0 &&
                 minusone != 0)
            return false;
        else if (minusone > 1 &&
                 one == 0)
            return false;

        return true;
    }

    // Driver Code
    public static void Main (String[] args)
    {
        int []arr = {0, 1, 1, 10};
        int n = arr.Length;
        if (checkArray(arr, n))
        Console.Write("Yes");
        else
        Console.Write("No");
    }
}

// This code is contributed by parashar....
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find if
// product of every pair
// is present in array.

// Returns true if product
// of every pair in arr[]
// is present in arr[]
function checkArray($arr , $n)
{
    // variable to store number
    // of zeroes, ones, minus
    // one and other numbers.
    $zero = 0; $one = 0;
    $minusone = 0; $other=0;
    for ($i = 0; $i < $n; $i++)
    {
        // incrementing the
        // variable values
        if ($arr[$i] == 0)
            $zero++;
        else if ($arr[$i] == 1)
            $one++;
        else if ($arr[$i] == -1)
            $minusone++;
        else
            $other++;
    }

    // checking the conditions
    if ($other > 1)
        return false;
    else if ($other != 0 &&
             $minusone != 0)
        return false;
    else if ($minusone > 1 &&
             $one == 0)
        return false;

    return true;
}

// Driver Code
{
    $arr = array(0, 1, 1, 10);
    $n = sizeof($arr) / sizeof($arr[0]);
    if (checkArray($arr, $n))
    echo "Yes";
    else
    echo "No";
    return 0;
}

//This code is contributed
// by nitin mittal.
?>
```

## java 描述语言

```
<script>
//javascript program to find if
// product of every pair
// is present in array.
// Returns true if product
// of every pair in arr[]
// is present in arr[]
function checkArray(arr,n)
{
    // variable to store number
    // of zeroes, ones, minus
    // one and other numbers.
    let zero = 0, one = 0,
        minusone = 0, other=0;
    for (let i = 0; i < n; i++)
    {
        // incrementing the
        // variable values
        if (arr[i] == 0)
            zero++;
        else if (arr[i] == 1)
            one++;
        else if (arr[i] == -1)
            minusone++;
        else
            other++;
    }

    // checking the conditions
    if (other > 1)
        return false;
    else if (other != 0 &&
            minusone != 0)
        return false;
    else if (minusone > 1 &&
            one == 0)
        return false;

    return true;
}

    let arr = [0, 1, 1, 10];
    let n = arr.length;
    if (checkArray(arr, n))
    document.write("Yes");
    else
    document.write("No");

// This code is contributed by vaibhavrabadiya117.
</script>
```

**输出:**

```
yes
```

本文由 **Ayush Jha** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。