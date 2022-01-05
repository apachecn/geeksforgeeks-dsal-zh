# 中间追加插入 MEX 形成的系列的第 k 个指标的值

> 原文:[https://www . geesforgeks . org/value-k-th-index-series-formed-append-insert-MEX-middle/](https://www.geeksforgeeks.org/value-k-th-index-series-formed-append-insert-mex-middle/)

给定两个整数，n 和 k。最初我们有一个由单个数字 1 组成的序列。我们需要考虑 n 步后形成的级数。在每一步中，我们将序列附加到自身，并在中间插入序列的 **MEX** (最小排除)(> 0)值。执行(n-1)个步骤。最后，找到结果序列的第 k 个索引的值。
示例:

```
Input : n = 3, k = 2.
Output: Initially, we have {1}, we have to perform 2 steps.
        1st step :  {1, 2, 1}, since MEX of {1} is 2.
        2nd step:   {1, 2, 1, 3, 1, 2, 1}, 
                     since MEX of {1, 2, 1} is 3.
        Value of 2nd Index = 2.

Input : n = 4, k = 8.
Output: Perform 3 steps.
        After second step, we have  {1, 2, 1, 3, 1, 2, 1}
        3rd step: {1, 2, 1, 3, 1, 2, 1, 4, 1, 2, 1, 3, 
                               1, 2, 1}, since MEX = 4.
        Value of 8th index = 4.
```

一个**简单的解决方案**是使用给定的步骤生成序列并存储在数组中。最后，我们返回数组的第 k 个元素。
一个**高效的解决方案**就是利用二分搜索法。观察我们的结果序列的中间元素是 n 本身。序列的长度是 2<sup>n</sup>–1，因为长度会像(1，3，7，15…)2<sup>n</sup>-1 一样。我们用二分搜索法来解决这个问题。我们知道，序列的中间元素是对其执行的步骤(从 1 开始)的编号。
事实上，序列中的每个元素都是某一步的中间元素。
我们从第 n 步开始搜索元素，如果找到了，我们将中间的索引与‘k’进行比较，如果找到了，我们返回 n，否则我们将 n 减 1，并更新我们的搜索范围。
我们重复这个步骤，直到达到索引。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to fin k-th element after append
// and insert middle operations
#include <bits/stdc++.h>
using namespace std;
void findElement(int n, int k)
{
    int ans = n; // Middle element of the sequence
    int left = 1;

    // length of the resulting sequence.
    int right = pow(2, n) - 1;
    while (1) {
        int mid = (left + right) / 2;
        if (k == mid) {
            cout << ans << endl;
            break;
        }

        // Updating the middle element of next sequence
        ans--;

        // Moving to the left side of the middle element.
        if (k < mid)
            right = mid - 1;

        // Moving to the right side of the middle element.
        else
            left = mid + 1;        
    }
}

// Driver code
int main()
{
    int n = 4, k = 8;
    findElement(n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to fin k-th element after append
// and insert middle operations

class GFG
{

    static void findElement(int n, int k)
    {
        // Middle element of the sequence
        int ans = n;
        int left = 1;

        // length of the resulting sequence.
        int right = (int) (Math.pow(2, n) - 1);
        while (true)
        {
            int mid = (left + right) / 2;
            if (k == mid)
            {
                System.out.println(ans);
                break;
            }

            // Updating the middle element
            // of next sequence
            ans--;

            // Moving to the left side of
            // the middle element.
            if (k < mid)
            {
                right = mid - 1;
            }

            // Moving to the right side of
            // the middle element.
            else
            {
                left = mid + 1;
            }
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 4, k = 8;
        findElement(n, k);
    }

}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 code to find k-th element after append
# and insert middle operations
import math

def findElement(n , k):
    ans = n      # Middle element of the sequence
    left = 1

    # length of the resulting sequence.
    right = math.pow(2, n) - 1
    while 1:
        mid = int((left + right) / 2)
        if k == mid:
            print(ans)
            break

        # Updating the middle element of next sequence
        ans-=1

        # Moving to the left side of the middle element.
        if k < mid:
            right = mid - 1

        # Moving to the right side of the middle element.
        else:
            left = mid + 1

# Driver code
n = 4
k = 8
findElement(n, k)

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# program to fin k-th element after append
// and insert middle operations
using System;

class GFG
{

    static void findElement(int n, int k)
    {
        // Middle element of the sequence
        int ans = n;
        int left = 1;

        // length of the resulting sequence.
        int right = (int) (Math.Pow(2, n) - 1);
        while (true)
        {
            int mid = (left + right) / 2;
            if (k == mid)
            {
                Console.WriteLine(ans);
                break;
            }

            // Updating the middle element
            // of next sequence
            ans--;

            // Moving to the left side of
            // the middle element.
            if (k < mid)
            {
                right = mid - 1;
            }

            // Moving to the right side of
            // the middle element.
            else
            {
                left = mid + 1;
            }
        }
    }

    // Driver code
    public static void Main()
    {
        int n = 4, k = 8;
        findElement(n, k);
    }

}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to fin k-th element
// after append and insert middle
// operations

function findElement($n, $k)
{

    // Middle element of the sequence
    $ans = $n;
    $left = 1;

    // length of the resulting sequence.
    $right = pow(2, $n) - 1;
    while (1)
    {
        $mid = ($left + $right) / 2;
        if ($k ==$mid)
        {
            echo $ans ,"\n";
            break;
        }

        // Updating the middle element
        // of next sequence
        $ans--;

        // Moving to the left side of
        // the middle element.
        if ($k < $id)
            $right = $mid - 1;

        // Moving to the right side
        // of the middle element.
        else
            $left = $mid + 1;    
    }
}

    // Driver code
    $n = 4;
    $k = 8;
    findElement($n, $k);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// JavaScript program to fin k-th element after append
// and insert middle operations

   function findElement(n, k)
    {
        // Middle element of the sequence
        let ans = n;
        let left = 1;

        // length of the resulting sequence.
        let right = (Math.pow(2, n) - 1);
        while (true)
        {
            let mid = (left + right) / 2;
            if (k == mid)
            {
                document.write(ans);
                break;
            }

            // Updating the middle element
            // of next sequence
            ans--;

            // Moving to the left side of
            // the middle element.
            if (k < mid)
            {
                right = mid - 1;
            }

            // Moving to the right side of
            // the middle element.
            else
            {
                left = mid + 1;
            }
        }
    }

// Driver code            
        let n = 4, k = 8;
        findElement(n, k);

         // This code is contributed by code_hunt.
</script>
```

**输出:**

```
4
```

**时间复杂度:** O(log n)