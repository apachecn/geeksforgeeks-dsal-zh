# 连续两次不跳过完成任务的最短时间

> 原文:[https://www . geesforgeks . org/最短完成任务时间-不跳过-连续两次/](https://www.geeksforgeeks.org/minimum-time-to-finish-tasks-without-skipping-two-consecutive/)

给定 n 个任务花费的时间。找到完成任务所需的最短时间，以便允许跳过任务，但不能跳过两个连续的任务。
**例:**

```
Input : arr[] = {10, 5, 7, 10}
Output : 12
We can skip first and last task and
finish these task in 12 min.

Input : arr[] = {10}
Output : 0
There is only one task and we can
skip it.

Input : arr[] = {10, 30}
Output : 10

Input : arr[] = {10, 5, 2, 4, 8, 6, 7, 10}
Output : 22
```

预期时间复杂度为 0(n)，额外空间为 0(1)。

给定的问题具有以下递归性质。让**最小时间(i)** 成为我完成任务的最短时间。它可以写成至少两个值。

1.  最小时间如果我的任务包含在列表中，让这个时间包含(I)
2.  最小时间如果我的任务被排除在结果之外，让这个时间被排除(I)

```
minTime(i) = min(excl(i), incl(i)) 
```

如果有 n 个任务，索引从 0 开始，结果为 **minTime(n-1)** 。
**include(I)**可以写成如下。

```
// There are two possibilities
// (a) Previous task is also included
// (b) Previous task is not included
incl(i) = min(incl(i-1), excl(i-1)) +
              arr[i] // Since this is inclusive 
                     // arr[i] must be included 
```

**不包括(i)** 可写如下。

```
// There is only one possibility (Previous task must be
// included as we can't skip consecutive tasks.
excl(i) = incl(i-1)  
```

一个简单的解决方案是制作两个包含[]和不包含[]的表来存储任务的时间。最终返回包含[n-1]和不包含[n-1]的最小值。这个解决方案需要 O(n)个时间和 O(n)个空间。
如果我们仔细看一下，可以发现我们只需要包含和不包含之前的工作。这样可以节省空间，在 O(n)时间和 O(1)空间内解决问题。下面是 C++实现的思路。

## C++

```
// C++ program to find minimum time to finish tasks
// such that no two consecutive tasks are skipped.
#include <bits/stdc++.h>
using namespace std;

// arr[] represents time taken by n given tasks
int minTime(int arr[], int n)
{
    // Corner Cases
    if (n <= 0)
        return 0;

    // Initialize value for the case when there
    // is only one task in task list.
    int incl = arr[0];  // First task is included
    int excl = 0;       // First task is exluded

    // Process remaining n-1 tasks
    for (int i=1; i<n; i++)
    {
       // Time taken if current task is included
       // There are two possibilities
       // (a) Previous task is also included
       // (b) Previous task is not included
       int incl_new = arr[i] + min(excl, incl);

       // Time taken when current task is not
       // included.  There is only one possibility
       // that previous task is also included.
       int excl_new = incl;

       // Update incl and excl for next iteration
       incl = incl_new;
       excl = excl_new;
    }

    // Return minimum of two values for last task
    return min(incl, excl);
}

// Driver code
int main()
{
    int arr1[] = {10, 5, 2, 7, 10};
    int n1 = sizeof(arr1)/sizeof(arr1[0]);
    cout << minTime(arr1, n1) << endl;

    int arr2[] = {10, 5, 7, 10};
    int n2 = sizeof(arr2)/sizeof(arr2[0]);
    cout << minTime(arr2, n2) << endl;

    int arr3[] = {10, 5, 2, 4, 8, 6, 7, 10};
    int n3 = sizeof(arr3)/sizeof(arr3[0]);
    cout << minTime(arr3, n3) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum time to
// finish tasks such that no two
// consecutive tasks are skipped.
import java.io.*;

class GFG {

    // arr[] represents time taken by n
    // given tasks
    static int minTime(int arr[], int n)
    {
        // Corner Cases
        if (n <= 0)
            return 0;

        // Initialize value for the case
        // when there is only one task in
        // task list.
        // First task is included
        int incl = arr[0];

        // First task is exluded
        int excl = 0;    

        // Process remaining n-1 tasks
        for (int i = 1; i < n; i++)
        {
        // Time taken if current task is
        // included. There are two
        // possibilities
        // (a) Previous task is also included
        // (b) Previous task is not included
        int incl_new = arr[i] + Math.min(excl,
                                       incl);

        // Time taken when current task is not
        // included. There is only one
        // possibility that previous task is
        // also included.
        int excl_new = incl;

        // Update incl and excl for next
        // iteration
        incl = incl_new;
        excl = excl_new;
        }

        // Return minimum of two values for
        // last task
        return Math.min(incl, excl);
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr1[] = {10, 5, 2, 7, 10};
        int n1 = arr1.length;
        System.out.println(minTime(arr1, n1));

        int arr2[] = {10, 5, 7, 10};
        int n2 = arr2.length;
        System.out.println(minTime(arr2, n2));

        int arr3[] = {10, 5, 2, 4, 8, 6, 7, 10};
        int n3 = arr3.length;
        System.out.println(minTime(arr3, n3));

    }
}
// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python3 program to find minimum
# time to finish tasks such that no
# two consecutive tasks are skipped.

# arr[] represents time
# taken by n given tasks
def minTime(arr, n):

    # Corner Cases
    if (n <= 0): return 0

    # Initialize value for the
    # case when there is only
    # one task in task list.
    incl = arr[0] # First task is included
    excl = 0      # First task is exluded

    # Process remaining n-1 tasks
    for i in range(1, n):

        # Time taken if current task is included
        # There are two possibilities
        # (a) Previous task is also included
        # (b) Previous task is not included
        incl_new = arr[i] + min(excl, incl)

        # Time taken when current task is not
        # included. There is only one possibility
        # that previous task is also included.
        excl_new = incl

        # Update incl and excl for next iteration
        incl = incl_new
        excl = excl_new

    # Return minimum of two values for last task
    return min(incl, excl)

# Driver code
arr1 = [10, 5, 2, 7, 10]
n1 = len(arr1)
print(minTime(arr1, n1))

arr2 = [10, 5, 7, 10]
n2 = len(arr2)
print(minTime(arr2, n2))

arr3 = [10, 5, 2, 4, 8, 6, 7, 10]
n3 = len(arr3)
print(minTime(arr3, n3))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to find minimum time to
// finish tasks such that no two
// consecutive tasks are skipped.
using System;

class GFG {

    // arr[] represents time taken by n
    // given tasks
    static int minTime(int []arr, int n)
    {
        // Corner Cases
        if (n <= 0)
            return 0;

        // Initialize value for the case
        // when there is only one task in
        // task list.
        // First task is included
        int incl = arr[0];

        // First task is exluded
        int excl = 0;    

        // Process remaining n-1 tasks
        for (int i = 1; i < n; i++)
        {
        // Time taken if current task is
        // included. There are two
        // possibilities
        // (a) Previous task is also included
        // (b) Previous task is not included
        int incl_new = arr[i] + Math.Min(excl,
                                       incl);

        // Time taken when current task is not
        // included. There is only one
        // possibility that previous task is
        // also included.
        int excl_new = incl;

        // Update incl and excl for next
        // iteration
        incl = incl_new;
        excl = excl_new;
        }

        // Return minimum of two values for
        // last task
        return Math.Min(incl, excl);
    }

    // Driver code
    public static void Main()
    {
        int []arr1 = {10, 5, 2, 7, 10};
        int n1 = arr1.Length;
        Console.WriteLine(minTime(arr1, n1));

        int []arr2 = {10, 5, 7, 10};
        int n2 = arr2.Length;
        Console.WriteLine(minTime(arr2, n2));

        int []arr3 = {10, 5, 2, 4, 8, 6, 7, 10};
        int n3 = arr3.Length;
        Console.WriteLine(minTime(arr3, n3));

    }
}
// This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum time
// to finish tasks such that no two
// consecutive tasks are skipped.

// arr[] represents time
// taken by n given tasks
function minTime($arr, $n)
{
    // Corner Cases
    if ($n <= 0)
        return 0;

    // Initialize value for the
    // case when there is only
    // one task in task list.

    // First task is included
    $incl = $arr[0];

    // First task is exluded
    $excl = 0;    

    // Process remaining n-1 tasks
    for ($i = 1; $i < $n; $i++)
    {
    // Time taken if current task is
    // included There are two possibilities
    // (a) Previous task is also included
    // (b) Previous task is not included
    $incl_new = $arr[$i] + min($excl, $incl);

    // Time taken when current task
    // is not included. There is only
    // one possibility that previous
    // task is also included.
    $excl_new = $incl;

    // Update incl and excl
    // for next iteration
    $incl = $incl_new;
    $excl = $excl_new;
    }

    // Return minimum of two
    // values for last task
    return min($incl, $excl);
}

// Driver code

$arr1 = array(10, 5, 2, 7, 10);
$n1 = sizeof($arr1);
echo minTime($arr1, $n1),"\n" ;

$arr2 = array(10, 5, 7, 10);
$n2 = sizeof($arr2);
echo minTime($arr2, $n2),"\n" ;

$arr3 = array(10, 5, 2, 4,
             8, 6, 7, 10);
$n3 = sizeof($arr3);
echo minTime($arr3, $n3);

// This code is contributed
// by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Javascript program to find minimum time to
// finish tasks such that no two
// consecutive tasks are skipped.

    // arr[] represents time taken by n
    // given tasks
    function minTime(arr, n)
    {
        // Corner Cases
        if (n <= 0)
            return 0;

        // Initialize value for the case
        // when there is only one task in
        // task list.
        // First task is included
        let incl = arr[0];

        // First task is exluded
        let excl = 0;    

        // Process remaining n-1 tasks
        for (let i = 1; i < n; i++)
        {
        // Time taken if current task is
        // included. There are two
        // possibilities
        // (a) Previous task is also included
        // (b) Previous task is not included
        let incl_new = arr[i] + Math.min(excl,
                                       incl);

        // Time taken when current task is not
        // included. There is only one
        // possibility that previous task is
        // also included.
        let excl_new = incl;

        // Update incl and excl for next
        // iteration
        incl = incl_new;
        excl = excl_new;
        }

        // Return minimum of two values for
        // last task
        return Math.min(incl, excl);
    }

// Driver Code

        let arr1 = [10, 5, 2, 7, 10];
        let n1 = arr1.length;
        document.write(minTime(arr1, n1) + "<br/>");

        let arr2 = [10, 5, 7, 10];
        let n2 = arr2.length;
        document.write(minTime(arr2, n2) + "<br/>");

        let arr3 = [10, 5, 2, 4, 8, 6, 7, 10];
        let n3 = arr3.length;
        document.write(minTime(arr3, n3) + "<br/>");      

</script>
```

**输出:**

```
12
12
22
```

**相关问题:**
[找到在给定约束条件下完成所有工作的最短时间](https://www.geeksforgeeks.org/find-minimum-time-to-finish-all-jobs-with-given-constraints/)
[最大和使得没有两个元素相邻。](https://www.geeksforgeeks.org/maximum-sum-such-that-no-two-elements-are-adjacent/)
本文由 **Arnab Dutta** 供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息