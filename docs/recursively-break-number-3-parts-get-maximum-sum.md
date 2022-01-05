# 递归地将一个数分成 3 部分，得到最大和

> 原文:[https://www . geesforgeks . org/递归-break-number-3-parts-get-maximum-sum/](https://www.geeksforgeeks.org/recursively-break-number-3-parts-get-maximum-sum/)

给定一个数 n，我们只能把它分成 n/2、n/3 和 n/4 三部分(我们只考虑整数部分)。任务是通过递归地将数分成三部分，然后将它们相加，找到我们能得到的最大和。
**例:**

```
Input : n = 12
Output : 13
// We break n = 12 in three parts {12/2, 12/3, 12/4} 
// = {6, 4, 3},  now current sum is = (6 + 4 + 3) = 13 
// again we break 6 = {6/2, 6/3, 6/4} = {3, 2, 1} = 3 + 
// 2 + 1 = 6 and further breaking 3, 2 and 1 we get maximum
// summation as 1, so breaking 6 in three parts produces
// maximum sum 6 only similarly breaking 4 in three   
// parts we can get maximum sum 4 and same for 3 also.
// Thus maximum sum by breaking number in parts  is=13

Input : n = 24
Output : 27
// We break n = 24 in three parts {24/2, 24/3, 24/4} 
// = {12, 8, 6},  now current sum is = (12 + 8 + 6) = 26
// As seen in example, recursively breaking 12 would
// produce value 13\. So our maximum sum is 13 + 8 + 6 = 27.
// Note that recursively breaking 8 and 6 doesn't produce
// more values, that is why they are not broken further.

Input : n = 23
Output : 23
// we break n = 23 in three parts {23/2, 23/3, 23/4} = 
// {10, 7, 5}, now current sum is = (10 + 7 + 5) = 22\. 
// Since  after further breaking we can not get maximum
// sum hence number is itself maximum i.e; answer is 23
```

这个问题的一个**简单的解决方法**就是递归**做**。在每次通话中，我们只需检查**max((max(n/2)+max(n/3)+max(n/4))、n)** 并返回。因为要么我们把数分成几部分就能得到最大和，要么数本身就是最大。下面是递归算法的实现。

## C++

```
// A simple recursive C++ program to find
// maximum sum by recursively breaking a
// number in 3 parts.
#include<bits/stdc++.h>
using namespace std;

// Function to find the maximum sum
int breakSum(int n)
{
    // base conditions
    if (n==0 || n == 1)
        return n;

    // recursively break the number and return
    // what maximum you can get
    return max((breakSum(n/2) + breakSum(n/3) +
                breakSum(n/4)),  n);
}

// Driver program to run the case
int main()
{
    int n = 12;
    cout << breakSum(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A simple recursive JAVA program to find
// maximum sum by recursively breaking a
// number in 3 parts.
import java.io.*;

class GFG {

    // Function to find the maximum sum
    static int breakSum(int n)
    {
        // base conditions
        if (n==0 || n == 1)
            return n;

        // recursively break the number and return
        // what maximum you can get
        return Math.max((breakSum(n/2) + breakSum(n/3) +
                    breakSum(n/4)),  n);   
    }

    // Driver program to test the above function
    public static void main (String[] args) {
        int n = 12;
        System.out.println(breakSum(n));
    }
}
// This code is contributed by Amit Kumar
```

## 蟒蛇 3

```
# A simple recursive Python3 program to
# find maximum sum by recursively breaking 
# a number in 3 parts.

# Function to find the maximum sum
def breakSum(n) :

    # base conditions
    if (n == 0 or n == 1) :
        return n

    # recursively break the number and
    # return what maximum you can get
    return max((breakSum(n // 2) +
                breakSum(n // 3) +
                breakSum(n // 4)), n)

# Driver Code
if __name__ == "__main__" :

    n = 12
    print(breakSum(n))

# This code is contributed by Ryuga
```

## C#

```
// A simple recursive C# program to find
// maximum sum by recursively breaking a
// number in 3 parts.
using System;

class GFG {

    // Function to find the maximum sum
    static int breakSum(int n)
    {
        // base conditions
        if (n==0 || n == 1)
            return n;

        // recursively break the number
        // and return what maximum you
        // can get
        return Math.Max((breakSum(n/2)
                       + breakSum(n/3)
                 + breakSum(n/4)), n);
    }

    // Driver program to test the
    // above function
    public static void Main ()
    {
        int n = 12;

        Console.WriteLine(breakSum(n));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A simple recursive PHP program to find
// maximum sum by recursively breaking a
// number in 3 parts.

// Function to find the maximum sum
function breakSum($n)
{
    // base conditions
    if ($n == 0 || $n == 1)
        return $n;

    // recursively break the number and
    // return what maximum you can get
    return max((breakSum(intval($n / 2)) +
                breakSum(intval($n / 3)) +
                breakSum(intval($n / 4))), $n);
}

// Driver program to run the case
$n = 12;
echo breakSum($n);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// A simple recursive Javascript program to find
// maximum sum by recursively breaking a
// number in 3 parts.

    // Function to find the maximum sum
    function breakSum(n)
    {
        // base conditions
        if (n==0 || n == 1)
            return n;

        // recursively break the number and return
        // what maximum you can get
        return Math.max((breakSum(Math.floor(n/2)) +
                    breakSum(Math.floor(n/3)) +
                    breakSum(Math.floor(n/4))),  n); 
    }

    // Driver program to test the above function

    let n = 12;
    document.write(breakSum(n));

    // This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
13
```

这个问题的一个有效解决方案是使用**动态编程**，因为在递归分解零件数量时，我们必须执行一些重叠的问题。例如，n = 30 的一部分将是{15，10，7}，15 的一部分将是{7，5，3}，因此我们必须重复 7 的过程两次以进一步打破。为了避免这种重叠问题，我们使用**动态编程**。我们将值存储在一个数组中，如果在递归调用中有任何数字，我们已经有了该数字的解，所以我们直接从数组中提取它。

## C++

```
// A Dynamic programming based C++ program
// to find maximum sum by recursively breaking
// a number in 3 parts.
#include<bits/stdc++.h>
#define MAX 1000000
using namespace std;

int breakSum(int n)
{
    int dp[n+1];

    // base conditions
    dp[0] = 0, dp[1] = 1;

    // Fill in bottom-up manner using recursive
    // formula.
    for (int i=2; i<=n; i++)
       dp[i] = max(dp[i/2] + dp[i/3] + dp[i/4], i);

    return dp[n];
}

// Driver program to run the case
int main()
{
    int n = 24;
    cout << breakSum(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A simple recursive JAVA program to find
// maximum sum by recursively breaking a
// number in 3 parts.
import java.io.*;

class GFG {

    final int MAX = 1000000;

    // Function to find the maximum sum
    static int breakSum(int n)
    {
        int dp[] = new int[n+1];

        // base conditions
        dp[0] = 0;  dp[1] = 1;

        // Fill in bottom-up manner using recursive
        // formula.
        for (int i=2; i<=n; i++)
           dp[i] = Math.max(dp[i/2] + dp[i/3] + dp[i/4], i);

        return dp[n];
    }

    // Driver program to test the above function
    public static void main (String[] args) {
        int n = 24;
        System.out.println(breakSum(n));
    }
}
// This code is contributed by Amit Kumar
```

## 蟒蛇 3

```
# A Dynamic programming based Python program
# to find maximum sum by recursively breaking
# a number in 3 parts.

MAX = 1000000

def breakSum(n):

    dp = [0]*(n+1)

    # base conditions
    dp[0] = 0
    dp[1] = 1

    # Fill in bottom-up manner using recursive
    # formula.
    for i in range(2, n+1):
        dp[i] = max(dp[int(i/2)] + dp[int(i/3)] + dp[int(i/4)], i);

    return dp[n]

# Driver program to run the case
n = 24
print(breakSum(n))

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// A simple recursive C# program to find
// maximum sum by recursively breaking a
// number in 3 parts.
using System;

class GFG {

    // Function to find the maximum sum
    static int breakSum(int n)
    {
        int []dp = new int[n+1];

        // base conditions
        dp[0] = 0; dp[1] = 1;

        // Fill in bottom-up manner
        // using recursive formula.
        for (int i = 2; i <= n; i++)
            dp[i] = Math.Max(dp[i/2] +
                  dp[i/3] + dp[i/4], i);

        return dp[n];
    }

    // Driver program to test the
    // above function
    public static void Main ()
    {
        int n = 24;
        Console.WriteLine(breakSum(n));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A Dynamic programming based PHP program
// to find maximum sum by recursively breaking
// a number in 3 parts.
function breakSum($n)
{
    $dp = array_fill(0, $n + 1, 0);

    // base conditions
    $dp[0] = 0;
    $dp[1] = 1;

    // Fill in bottom-up manner using
    // recursive formula.
    for ($i = 2; $i <= $n; $i++)
    $dp[$i] = max($dp[(int)($i / 2)] +
                  $dp[(int)($i / 3)] +
                  $dp[(int)($i / 4)], $i);

    return $dp[$n];
}

// Driver Code
$n = 24;
echo breakSum($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// A simple recursive JAVASCRIPT program to find
// maximum sum by recursively breaking a
// number in 3 parts.

    let MAX = 1000000;
    // Function to find the maximum sum
    function breakSum(n)
    {
        let dp=new Array(n+1);
        for(let i=0;i<dp;i++)
        {
            dp[i]=0;
        }
        // base conditions
        dp[0] = 0;  dp[1] = 1;

        // Fill in bottom-up manner using recursive
        // formula.
        for (let i=2; i<=n; i++)
           dp[i] = Math.max(dp[Math.floor(i/2)] +
           dp[Math.floor(i/3)] + dp[Math.floor(i/4)], i);

        return dp[n];
    }

    // Driver program to test the above function
    let n = 24;
    document.write(breakSum(n));

    // This code is contributed by rag2127

</script>
```

**输出:**

```
27
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)
本文由 [**沙莎克·米什拉(古鲁)**](https://www.facebook.com/shashank.mishra.92167) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。