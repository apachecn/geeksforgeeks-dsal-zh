# 排序数组中的绝对不同计数

> 原文:[https://www . geesforgeks . org/absolute-distinct-count-array-sorted-absolute-values/](https://www.geeksforgeeks.org/absolute-distinct-count-array-sorted-absolute-values/)

给定一个排序的整数数组，返回数组元素中不同绝对值的个数。输入可以包含重复的值。
**例:**

```
Input: [-3, -2, 0, 3, 4, 5]
Output: 5
There are 5 distinct absolute values
among the elements of this array, i.e.
0, 2, 3, 4 and 5)

Input:  [-1, -1, -1, -1, 0, 1, 1, 1, 1]
Output: 2

Input:  [-1, -1, -1, -1, 0]
Output: 2

Input:  [0, 0, 0]
Output: 1 
```

解决方案应该只对输入数组进行一次扫描，并且不应该使用任何额外的空间。即期望时间复杂度为 O(n)，辅助空间为 O(1)。

一个简单的解决方案是使用 set。对于输入数组的每个元素，我们在集合中插入它的绝对值。由于 set 不支持重复元素，元素的绝对值将只插入一次。因此，所需的计数是集合的大小。
下面是想法的实现。

## C++

```
// C++ program to find absolute distinct
// count of an array in O(n) time.
#include <bits/stdc++.h>
using namespace std;

// The function returns number of
// distinct absolute values among
// the elements of the array
int distinctCount(int arr[], int n)
{
    unordered_set<int> s;

    // Note that set keeps only one
    // copy even if we try to insert
    // multiple values
    for (int i = 0 ; i < n; i++)
        s.insert(abs(arr[i]));

    return s.size();
}

// Driver code
int main()
{
    int arr[] = {-2, -1, 0, 1, 1};
    int n = sizeof(arr)/sizeof(arr[0]);

    cout << "Count of absolute distinct values : "
         << distinctCount(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java code to find absolute distinct
// count of an array in O(n) time.
import java.util.*;

class GFG
{
    // The function returns number of
    // distinct absolute values among
    // the elements of the array
    static int distinctCount(int arr[], int n)
    {
        Set<Integer> s = new HashSet<Integer> ();

        // Note that set keeps only one
        // copy even if we try to insert
        // multiple values
        for (int i = 0 ; i < n; i++)
        s.add(Math.abs(arr[i]));

        return s.size();

    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {-2, -1, 0, 1, 1};
        int n = arr.length;

        System.out.println("Count of absolute distinct values : "
                           + distinctCount(arr, n));

    }
}

// This code is contributed by prerna saini
```

## 蟒蛇 3

```
# Python3 code to find absolute distinct
# count of an array in O(n) time.

# This function returns number of
# distinct absolute values among
# the elements of the array
def distinctCount(arr, n):
    s = set()

    # set keeps all unique elements
    for i in range(n):
        s.add(abs(arr[i]))
    return len(s)

# Driver Code
arr = [-2, -1, 0, 1, 1]
n = len(arr)
print("Count of absolute distinct values:",
                     distinctCount(arr, n))

# This code is contributed
# by Adarsh_Verma
```

## C#

```

// C# code to find absolute distinct
// count of an array in O(n) time.
using System;
using System.Collections.Generic;

class GFG
{
    // The function returns number of
    // distinct absolute values among
    // the elements of the array
    static int distinctCount(int []arr, int n)
    {
        HashSet<int> s = new HashSet<int>();

        // Note that set keeps only one
        // copy even if we try to insert
        // multiple values
        for (int i = 0 ; i < n; i++)
        s.Add(Math.Abs(arr[i]));

        return s.Count;

    }

    // Driver code
    public static void Main()
    {
        int []arr = {-2, -1, 0, 1, 1};
        int n = arr.Length;

        Console.Write("Count of absolute distinct values : "
                        + distinctCount(arr, n));

    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
    // Javascript code to find absolute distinct
    // count of an array in O(n) time.

    // The function returns number of
    // distinct absolute values among
    // the elements of the array
    function distinctCount(arr, n)
    {
        let s = new Set();

        // Note that set keeps only one
        // copy even if we try to insert
        // multiple values
        for (let i = 0 ; i < n; i++)
            s.add(Math.abs(arr[i]));

        return s.size;  
    }

    let arr = [-2, -1, 0, 1, 1];
    let n = arr.length;

    document.write("Count of absolute distinct values : "
                       + distinctCount(arr, n));

</script>
```

**输出:**

```
Count of absolute distinct values : 3
```

**时间复杂度:** O(n)
**辅助空间:** O(n)
**以上实现占用 O(n)个额外空间，在 O(1)个额外空间怎么做？**
想法是利用数组已经排序的事实。我们将不同元素的计数初始化为数组中的元素数。我们从数组两个角的两个索引变量开始，检查输入数组中 sum 为 0 的对。如果找到与 0 和的配对或遇到重复，我们减少不同元素的计数。最后，我们返回更新的计数。
以下是上述方法的实施。

## C++

```
// C++ program to find absolute distinct
// count of an array using O(1) space.
#include <bits/stdc++.h>
using namespace std;

// The function returns return number
// of distinct absolute values
// among the elements of the array
int distinctCount(int arr[], int n)
{
    // initialize count as number of elements
    int count = n;
    int i = 0, j = n - 1, sum = 0;

    while (i < j)
    {
        // Remove duplicate elements from the
        // left of the current window (i, j)
        // and also decrease the count
        while (i != j && arr[i] == arr[i + 1])
            count--, i++;

        // Remove duplicate elements from the
        // right of the current window (i, j)
        // and also decrease the count
        while (i != j && arr[j] == arr[j - 1])
            count--, j--;

        // break if only one element is left
        if (i == j)
            break;

        // Now look for the zero sum pair
        // in current window (i, j)
        sum = arr[i] + arr[j];

        if (sum == 0)
        {
            // decrease the count if (positive,
            // negative) pair is encountered
            count--;
            i++, j--;
        }
        else if(sum < 0)
            i++;
        else
            j--;
    }

    return count;
}

// Driver code
int main()
{
    int arr[] = {-2, -1, 0, 1, 1};
    int n = sizeof(arr)/sizeof(arr[0]);

    cout << "Count of absolute distinct values : "
         << distinctCount(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find absolute distinct
// count of an array using O(1) space.

import java.io.*;

class GFG {

// The function returns return number
// of distinct absolute values
// among the elements of the array
static int distinctCount(int arr[], int n)
{
    // initialize count as number of elements
    int count = n;
    int i = 0, j = n - 1, sum = 0;

    while (i < j)
    {
        // Remove duplicate elements from the
        // left of the current window (i, j)
        // and also decrease the count
        while (i != j && arr[i] == arr[i + 1])
        {
            count--;
            i++;
        }
        // Remove duplicate elements from the
        // right of the current window (i, j)
        // and also decrease the count
        while (i != j && arr[j] == arr[j - 1])
        {
            count--;
            j--;
        }
        // break if only one element is left
        if (i == j)
            break;

        // Now look for the zero sum pair
        // in current window (i, j)
        sum = arr[i] + arr[j];

        if (sum == 0)
        {
            // decrease the count if (positive,
            // negative) pair is encountered
            count--;
            i++;
            j--;
        }
        else if(sum < 0)
            i++;
        else
            j--;
    }

    return count;
}

// Driver code

    public static void main (String[] args) {

    int arr[] = {-2, -1, 0, 1, 1};
    int n = arr.length;

    System.out.println ("Count of absolute distinct values : "+
             distinctCount(arr, n));

    }
}
```

## 蟒蛇 3

```
# Python3 program to find absolute distinct
# count of an array using O(1) space.

# The function returns return number
# of distinct absolute values
# among the elements of the array
def distinctCount(arr, n):

    # initialize count as number of elements
    count = n;
    i = 0; j = n - 1; sum = 0;

    while (i < j):

        # Remove duplicate elements from the
        # left of the current window (i, j)
        # and also decrease the count
        while (i != j and arr[i] == arr[i + 1]):
            count = count - 1;
            i = i + 1;

        # Remove duplicate elements from the
        # right of the current window (i, j)
        # and also decrease the count
        while (i != j and arr[j] == arr[j - 1]):
            count = count - 1;
            j = j - 1;

        # break if only one element is left
        if (i == j):
            break;

        # Now look for the zero sum pair
        # in current window (i, j)
        sum = arr[i] + arr[j];

        if (sum == 0):

            # decrease the count if (positive,
            # negative) pair is encountered
            count = count - 1;
            i = i + 1;
            j = j - 1;

        elif(sum < 0):
            i = i + 1;
        else:
            j = j - 1;

    return count;

# Driver code
arr = [-2, -1, 0, 1, 1];
n = len(arr);

print("Count of absolute distinct values : ",
                      distinctCount(arr, n));

# This code is contributed
# by Akanksha Rai
```

## C#

```
//C# program to find absolute distinct
// count of an array using O(1) space.
using System;

class GFG {

// The function returns return number
// of distinct absolute values
// among the elements of the array
static int distinctCount(int []arr, int n)
{
    // initialize count as number of elements
    int count = n;
    int i = 0, j = n - 1, sum = 0;

    while (i < j)
    {
        // Remove duplicate elements from the
        // left of the current window (i, j)
        // and also decrease the count
        while (i != j && arr[i] == arr[i + 1])
        {
            count--;
            i++;
        }
        // Remove duplicate elements from the
        // right of the current window (i, j)
        // and also decrease the count
        while (i != j && arr[j] == arr[j - 1])
        {
            count--;
            j--;
        }
        // break if only one element is left
        if (i == j)
            break;

        // Now look for the zero sum pair
        // in current window (i, j)
        sum = arr[i] + arr[j];

        if (sum == 0)
        {
            // decrease the count if (positive,
            // negative) pair is encountered
            count--;
            i++;
            j--;
        }
        else if(sum < 0)
            i++;
        else
            j--;
    }

    return count;
}

// Driver code

    public static void Main () {

    int []arr = {-2, -1, 0, 1, 1};
    int n = arr.Length;

    Console.WriteLine("Count of absolute distinct values : "+
            distinctCount(arr, n));

    // This code is contributed by inder_verma   
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find absolute distinct
// count of an array using O(1) space.

// The function returns return number
// of distinct absolute values
// among the elements of the array
function distinctCount($arr, $n)
{
    // initialize count as number
    // of elements
    $count = $n;
    $i = 0; $j = $n - 1; $sum = 0;

    while ($i < $j)
    {
        // Remove duplicate elements from the
        // left of the current window (i, j)
        // and also decrease the count
        while ($i != $j && $arr[$i] == $arr[$i + 1])
            {$count--; $i++;}

        // Remove duplicate elements from the
        // right of the current window (i, j)
        // and also decrease the count
        while ($i != $j && $arr[$j] == $arr[$j - 1])
            {$count--; $j--;}

        // break if only one element is left
        if ($i == $j)
            break;

        // Now look for the zero sum pair
        // in current window (i, j)
        $sum = $arr[$i] + $arr[$j];

        if ($sum == 0)
        {
            // decrease the count if (positive,
            // negative) pair is encountered
            $count--;
            $i++; $j--;
        }
        else if($sum < 0)
            $i++;
        else
            $j--;
    }

    return $count;
}

// Driver code
$arr = array(-2, -1, 0, 1, 1);
$n = sizeof($arr);

echo "Count of absolute distinct values : " .
                     distinctCount($arr, $n);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
    // Javascript program to find absolute distinct
    // count of an array using O(1) space.

    // The function returns return number
    // of distinct absolute values
    // among the elements of the array
    function distinctCount(arr, n)
    {
        // initialize count as number of elements
        let count = n;
        let i = 0, j = n - 1, sum = 0;

        while (i < j)
        {
            // Remove duplicate elements from the
            // left of the current window (i, j)
            // and also decrease the count
            while (i != j && arr[i] == arr[i + 1])
                count--, i++;

            // Remove duplicate elements from the
            // right of the current window (i, j)
            // and also decrease the count
            while (i != j && arr[j] == arr[j - 1])
                count--, j--;

            // break if only one element is left
            if (i == j)
                break;

            // Now look for the zero sum pair
            // in current window (i, j)
            sum = arr[i] + arr[j];

            if (sum == 0)
            {
                // decrease the count if (positive,
                // negative) pair is encountered
                count--;
                i++, j--;
            }
            else if(sum < 0)
                i++;
            else
                j--;
        }

        return count;
    }

    let arr = [-2, -1, 0, 1, 1];
    let n = arr.length;

    document.write(
    "Count of absolute distinct values : " + distinctCount(arr, n));

</script>
```

**输出:**

```
Count of absolute distinct values : 3
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)
本文由 **Aditya Goel** 供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息