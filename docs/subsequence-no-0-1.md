# 1 后无 0 的最长子序列

> 原文:[https://www.geeksforgeeks.org/subsequence-no-0-1/](https://www.geeksforgeeks.org/subsequence-no-0-1/)

给定一个二进制数组，求最长子序列的长度，使得 1 后面没有 0。

**示例:**

```
Input : 1 1 0 1
Output : 3
Explanation : 
If we remove 0 from the array, then no
zero comes right after one (satisfying 
the condition) and the maximum game 
left are 3 (i.e. 1 1 1)

Input : 0
Output : 1
Explanation : 
Since he wants to save maximum game in
the array. He doesn't remove any game. 
```

让我们找出这个序列中有多少个 0，然后取最后一个 0 之后的所有 1。在每一步中，从序列的开始处取下一个零，并对其后的零进行计数。用最大值更新答案。
可以预先计算后缀上的 1 个数。
例如**0 1 0 1 1 1**
计算完后缀后，数组变成:
**0 4 0 3 2 1**
从开始移动到结束，每次在数组中发现零时，将零的数量增加 1。如果数组[索引]不为零，则 res = max(res，零的个数+该索引处的数组值)。
然后在循环之后:res = max(res，零的个数)

## C++

```
// CPP program to find longest subsequence
// such that there is no 0 after 1.
#include <bits/stdc++.h>
using namespace std;

int maxSubseq(int vec[], int n) {   

    // Store the count of number of ones
    // from right to left in the array
    int suffix = 0;
    for (int i = n - 1; i >= 0; i--)
    {
        if (vec[i] == 1)
        {
            suffix++;
            vec[i] = suffix;
        }
    }

    // Traverse from left to right, keep count
    // of 0s and for every 0, check number of
    // 1s after it. Update the result if needed.
    int res = 0;
    int zero = 0;   
    for (int i = 0; i < n; i++)
    {
        if (vec[i] == 0)
            zero++;

        // Checking the maximum size
        if (vec[i] > 0)
            res = max(res, zero + vec[i]);
    }

    // Checking the maximum size
    return max(res, zero);
}

// Driver Code
int main()
{
    int input[] = { 0, 1, 0, 0, 1, 0 };
    int n = sizeof(input) / sizeof(input[0]);   
    cout << maxSubseq(input, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to find longest subsequence
// such that there is no 0 after 1.
import java.io.*;

public class GFG {

    static int maxSubseq(int []vec, int n)
    {

        // Store the count of number of
        // ones from right to left in
        // the array
        int suffix = 0;

        for (int i = n - 1; i >= 0; i--)
        {
            if (vec[i] == 1)
            {
                suffix++;
                vec[i] = suffix;
            }
        }

        // Traverse from left to right, keep
        // count of 0s and for every 0, check
        // number of 1s after it. Update the
        // result if needed.
        int res = 0;
        int zero = 0;

        for (int i = 0; i < n; i++)
        {
            if (vec[i] == 0)
                zero++;

            // Checking the maximum size
            if (vec[i] > 0)
                res = Math.max(res, zero + vec[i]);
        }

        // Checking the maximum size
        return Math.max(res, zero);
    }

    // Driver Code
    static public void main (String[] args)
    {

        int []input = { 0, 1, 0, 0, 1, 0 };
        int n = input.length;

        System.out.println(maxSubseq(input, n));
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python 3 program to find longest subsequence
# such that there is no 0 after 1.

def maxSubseq(vec, n):
    # Store the count of number of ones
    # from right to left in the array
    suffix = 0
    i = n-1
    while(i >= 0):
        if (vec[i] == 1):
            suffix += 1
            vec[i] = suffix
        i -= 1

    # Traverse from left to right, keep count
    # of 0s and for every 0, check number of
    # 1s after it. Update the result if needed.
    res = 0
    zero = 0
    for i in range(0,n,1):
        if (vec[i] == 0):
            zero += 1

        # Checking the maximum size
        if (vec[i] > 0):
            res = max(res, zero + vec[i])

    # Checking the maximum size
    return max(res, zero)

# Driver code
 if __name__ == '__main__':
    input = [0, 1, 0, 0, 1, 0]
    n = len(input)
    print(maxSubseq(input, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find longest subsequence
// such that there is no 0 after 1.
using System;

public class GFG {

    static int maxSubseq(int []vec, int n)
    {

        // Store the count of number of
        // ones from right to left in
        // the array
        int suffix = 0;

        for (int i = n - 1; i >= 0; i--)
        {
            if (vec[i] == 1)
            {
                suffix++;
                vec[i] = suffix;
            }
        }

        // Traverse from left to right, keep
        // count of 0s and for every 0, check
        // number of 1s after it. Update the
        // result if needed.
        int res = 0;
        int zero = 0;

        for (int i = 0; i < n; i++)
        {
            if (vec[i] == 0)
                zero++;

            // Checking the maximum size
            if (vec[i] > 0)
                res = Math.Max(res, zero + vec[i]);
        }

        // Checking the maximum size
        return Math.Max(res, zero);
    }

    // Driver Code

    static public void Main ()
    {

        int []input = { 0, 1, 0, 0, 1, 0 };
        int n = input.Length;

        Console.WriteLine(maxSubseq(input, n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find longest
// subsequence such that there
// is no 0 after 1.

function maxSubseq($vec, $n)
{

    // Store the count of
    // number of ones from
    // right to left in
    // the array
    $suffix = 0;
    for ($i = $n - 1;
         $i >= 0; $i--)
    {
        if ($vec[$i] == 1)
        {
            $suffix++;
            $vec[$i] = $suffix;
        }
    }

    // Traverse from left to
    // right, keep count of
    // 0s and for every 0,
    // check number of 1s after
    // it. Update the result if
    // needed.
    $res = 0;
    $zero = 0;
    for ($i = 0; $i < $n; $i++)
    {
        if ($vec[$i] == 0)
            $zero++;

        // Checking the
        // maximum size
        if ($vec[$i] > 0)
            $res = max($res, $zero +
                             $vec[$i]);
    }

    // Checking the
    // maximum size
    return max($res, $zero);
}

// Driver Code
$input = array(0, 1, 0, 0, 1, 0);
$n = count($input);
echo maxSubseq($input, $n);

// This code is contributed
// by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Javascript program to find longest subsequence
    // such that there is no 0 after 1.

    function maxSubseq(vec, n)
    {

        // Store the count of number of
        // ones from right to left in
        // the array
        let suffix = 0;

        for (let i = n - 1; i >= 0; i--)
        {
            if (vec[i] == 1)
            {
                suffix++;
                vec[i] = suffix;
            }
        }

        // Traverse from left to right, keep
        // count of 0s and for every 0, check
        // number of 1s after it. Update the
        // result if needed.
        let res = 0;
        let zero = 0;

        for (let i = 0; i < n; i++)
        {
            if (vec[i] == 0)
                zero++;

            // Checking the maximum size
            if (vec[i] > 0)
                res = Math.max(res, zero + vec[i]);
        }

        // Checking the maximum size
        return Math.max(res, zero);
    }

    let input = [ 0, 1, 0, 0, 1, 0 ];
    let n = input.length;

    document.write(maxSubseq(input, n));

</script>
```

**输出:**

```
4
```

本文由**沙钦·毕斯特**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。