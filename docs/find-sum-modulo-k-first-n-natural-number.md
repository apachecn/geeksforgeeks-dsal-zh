# 求前 N 个自然数的模 K 之和

> 原文:[https://www . geesforgeks . org/find-sum-modal-k-first-n-自然数/](https://www.geeksforgeeks.org/find-sum-modulo-k-first-n-natural-number/)

给定两个整数 **N** 和 **K** ，任务是求前 N 个自然数的模 K 之和，即 1%K + 2%K + …..+ N%K

**示例:**

```
Input : N = 10 and K = 2.
Output : 5
Sum = 1%2 + 2%2 + 3%2 + 4%2 + 5%2 + 6%2 +
      7%2 + 8%2 + 9%2 + 10%2
   = 1 + 0 + 1 + 0 + 1 + 0 + 1 + 0 + 1 + 0
   = 5.
```

**方法 1:**

将变量 I 从 1 迭代到 N，计算并添加 i%K

下面是该方法的实现:

## C++

```
// C++ program to find sum of
// modulo K of first N natural numbers.
#include <bits/stdc++.h>
using namespace std;

// Return sum of modulo K of
// first N natural numbers.
int findSum(int N, int K)
{
    int ans = 0;

    // Iterate from 1 to N &&
    // evaluating and adding i % K.
    for (int i = 1; i <= N; i++)
        ans += (i % K);

    return ans;
}

// Driver Program
int main()
{
    int N = 10, K = 2;
    cout << findSum(N, K) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of modulo
// K of first N natural numbers.
import java.io.*;

class GFG {

    // Return sum of modulo K of
    // first N natural numbers.
    static int findSum(int N, int K)
    {
        int ans = 0;

        // Iterate from 1 to N && evaluating
        // and adding i % K.
        for (int i = 1; i <= N; i++)
            ans += (i % K);

        return ans;
    }

    // Driver program
    static public void main(String[] args)
    {
        int N = 10, K = 2;
        System.out.println(findSum(N, K));
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 program to find sum
# of modulo K of first N
# natural numbers.

# Return sum of modulo K of
# first N natural numbers.

def findSum(N, K):
    ans = 0;

    # Iterate from 1 to N &&
    # evaluating and adding i % K.
    for i in range(1, N + 1):
        ans += (i % K);

    return ans;

# Driver Code
N = 10;
K = 2;
print(findSum(N, K));

# This code is contributed by mits
```

## C#

```
// C# program to find sum of modulo
// K of first N natural numbers.
using System;

class GFG {

    // Return sum of modulo K of
    // first N natural numbers.
    static int findSum(int N, int K)
    {
        int ans = 0;

        // Iterate from 1 to N && evaluating
        // and adding i % K.
        for (int i = 1; i <= N; i++)
            ans += (i % K);

        return ans;
    }

    // Driver program
    static public void Main()
    {
        int N = 10, K = 2;
        Console.WriteLine(findSum(N, K));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum
// of modulo K of first N
// natural numbers.

// Return sum of modulo K of
// first N natural numbers.

function findSum($N, $K)
{
    $ans = 0;

    // Iterate from 1 to N &&
    // evaluating and adding i % K.
    for ($i = 1; $i <= $N; $i++)
        $ans += ($i % $K);

    return $ans;
}

// Driver Code
$N = 10; $K = 2;
echo findSum($N, $K), "\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// JavaScript program to find sum
// of modulo K of first N natural
// numbers.

// Return sum of modulo K of
// first N natural numbers.
function findSum(N, K)
{
    let ans = 0;

    // Iterate from 1 to N && evaluating
    // and adding i % K.
    for(let i = 1; i <= N; i++)
        ans += (i % K);

    return ans;
}

// Driver Code
let N = 10, K = 2;

document.write(findSum(N, K));

// This code is contributed by code_hunt

</script>
```

**输出:**

```
5
```

**时间复杂度:** O(N)。

**方法二:**
此法出现两种情况。
情况 1:当 **N < K** 时，对于每个数字 I，N > = i > = 1，以 K 为模运算时会给出 I 作为结果，因此，所需的和将是前 N 个自然数 N*(N+1)/2 的和。
情况二:当 **N > = K** 时，自然数序列中从 1 到 K 的整数将产生，1，2，3，…..当以 K 为模运算时，结果为 K–1，0。同样，从 K + 1 到 2K，将产生相同的结果。因此，我们的想法是计算这个序列出现的次数，并将其与前 K–1 个自然数的总和相乘。

下面是该方法的实现:

## C++

```
// C++ program to find sum of modulo
// K of first N natural numbers.
#include <bits/stdc++.h>
using namespace std;

// Return sum of modulo K of
// first N natural numbers.
int findSum(int N, int K)
{
    int ans = 0;

    // Counting the number of times 1, 2, ..,
    // K-1, 0 sequence occurs.
    int y = N / K;

    // Finding the number of elements left which
    // are incomplete of sequence Leads to Case 1 type.
    int x = N % K;

    // adding multiplication of number of
    // times 1, 2, .., K-1, 0 sequence occurs
    // and sum of first k natural number and sequence
    // from case 1.
    ans = (K * (K - 1) / 2) * y + (x * (x + 1)) / 2;

    return ans;
}

// Driver program
int main()
{
    int N = 10, K = 2;
    cout << findSum(N, K) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of modulo
// K of first N natural numbers.
import java.io.*;

class GFG {

    // Return sum of modulo K of
    // first N natural numbers.
    static int findSum(int N, int K)
    {
        int ans = 0;

        // Counting the number of times 1, 2, ..,
        // K-1, 0 sequence occurs.
        int y = N / K;

        // Finding the number of elements left which
        // are incomplete of sequence Leads to Case 1 type.
        int x = N % K;

        // adding multiplication of number of times
        // 1, 2, .., K-1, 0 sequence occurs and sum
        // of first k natural number and sequence
        // from case 1.
        ans = (K * (K - 1) / 2) * y + (x * (x + 1)) / 2;

        return ans;
    }

    // Driver program
    static public void main(String[] args)
    {
        int N = 10, K = 2;
        System.out.println(findSum(N, K));
    }
}

// This Code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 program to find sum of modulo
# K of first N natural numbers.

# Return sum of modulo K of
# first N natural numbers.
def findSum(N, K):

    ans = 0;

    # Counting the number of times
    # 1, 2, .., K-1, 0 sequence occurs.
    y = N / K;

    # Finding the number of elements
    # left which are incomplete of
    # sequence Leads to Case 1 type.
    x = N % K;

    # adding multiplication of number
    # of times 1, 2, .., K-1, 0
    # sequence occurs and sum of
    # first k natural number and
    # sequence from case 1.
    ans = ((K * (K - 1) / 2) * y +
                (x * (x + 1)) / 2);

    return int(ans);

# Driver Code
N = 10;
K = 2;
print(findSum(N, K));

# This code is contributed by mits
```

## C#

```
// C# program to find sum of modulo
// K of first N natural numbers.
using System;

class GFG {

    // Return sum of modulo K of
    // first N natural numbers.
    static int findSum(int N, int K)
    {
        int ans = 0;

        // Counting the number of times 1, 2, ..,
        // K-1, 0 sequence occurs.
        int y = N / K;

        // Finding the number of elements left which
        // are incomplete of sequence Leads to Case 1 type.
        int x = N % K;

        // adding multiplication of number of times
        // 1, 2, .., K-1, 0 sequence occurs and sum
        // of first k natural number and sequence
        // from case 1.
        ans = (K * (K - 1) / 2) * y + (x * (x + 1)) / 2;

        return ans;
    }

    // Driver program
    static public void Main()
    {
        int N = 10, K = 2;
        Console.WriteLine(findSum(N, K));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum of modulo
// K of first N natural numbers.

// Return sum of modulo K of
// first N natural numbers.
function findSum($N, $K)
{
    $ans = 0;

    // Counting the number of times
    // 1, 2, .., K-1, 0 sequence occurs.
    $y = $N / $K;

    // Finding the number of elements
    // left which are incomplete of
    // sequence Leads to Case 1 type.
    $x = $N % $K;

    // adding multiplication of number
    // of times 1, 2, .., K-1, 0
    // sequence occurs and sum of
    // first k natural number and
    // sequence from case 1.
    $ans = ($K * ($K - 1) / 2) * $y
                 + ($x * ($x + 1)) / 2;

    return $ans;
}

// Driver program
    $N = 10; $K = 2;
    echo findSum($N, $K) ;

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program to find sum of modulo
// K of first N natural numbers.

// Return sum of modulo K of
// first N natural numbers.
function findSum(N, K)
{
    let ans = 0;

    // Counting the number of times
    // 1, 2, .., K-1, 0 sequence occurs.
    let y = N / K;

    // Finding the number of elements
    // left which are incomplete of
    // sequence Leads to Case 1 type.
    let x = N % K;

    // adding multiplication of number
    // of times 1, 2, .., K-1, 0
    // sequence occurs and sum of
    // first k natural number and
    // sequence from case 1.
    ans = (K * (K - 1) / 2) * y +
          (x * (x + 1)) / 2;

    return ans;
}

// Driver code
let N = 10;
let K = 2;

document.write(findSum(N, K));

// This code is contributed by _saurabh_jaiswal

</script>
```

**输出:**

```
5
```

**时间复杂度:** O(1)。

本文由 [**Anuj Chauhan**](https://web.facebook.com/anuj0503) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。