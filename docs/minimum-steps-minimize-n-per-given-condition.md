# 根据给定条件最小化 n 的最小步骤

> 原文:[https://www . geesforgeks . org/minimum-steps-minimum-n-per-给定条件/](https://www.geeksforgeeks.org/minimum-steps-minimize-n-per-given-condition/)

给定一个数字 n，根据以下标准计算最小步数，使其最小化为 1:

*   如果 n 能被 2 整除，那么我们可以把 n 减少到 n/2。
*   如果 n 能被 3 整除，那么你可以把 n 减少到 n/3。
*   n 减 1。

**示例:**

```
Input : n = 10
Output : 3

Input : 6
Output : 2
```

**贪婪方法(并不总是有效):**

按照**贪婪的方法**我们可以选择使 n 尽可能低的步长，并继续下去，直到它达到 1。

```
while ( n > 1)
{
    if (n % 3 == 0)
        n /= 3;    
    else if (n % 2 == 0)
        n /= 2;
    else
        n--;
    steps++;
}
```

如果我们仔细观察，贪婪策略在这里不起作用。
例:给定 n = 10，Greedy–>10/2 = 5-1 = 4/2 = 2/2 = 1(4 步)。
但最佳方式是–>10-1 = 9/3 = 3/3 = 1(3 步)。
所以，我们必须想出一个动态的方法来获得最优解。

**动态方法:**
对于寻找最小步长，我们有三种可能性，它们是:

```
f(n) = 1 + f(n-1)
f(n) = 1 + f(n/2) // if n is divisible by 2
f(n) = 1 + f(n/3) // if n is divisible by 3
```

**下面是上述递归公式的基于记忆的实现。**

## C++

```
// CPP program to minimize n to 1 by given
// rule in minimum steps
#include <bits/stdc++.h>
using namespace std;

// function to calculate min steps
int getMinSteps(int n, int *memo)
{
    // base case
    if (n == 1)
       return 0;
    if (memo[n] != -1)
       return memo[n];

    // store temp value for n as min( f(n-1),
    // f(n/2), f(n/3)) +1
    int res = getMinSteps(n-1, memo);

    if (n%2 == 0)
        res = min(res, getMinSteps(n/2, memo));
    if (n%3 == 0)
        res = min(res, getMinSteps(n/3, memo));

    // store memo[n] and return
    memo[n] = 1 + res;
    return memo[n];
}

// This function mainly initializes memo[] and
// calls getMinSteps(n, memo)
int getMinSteps(int n)
{
    int memo[n+1];

    // initialize memoized array
    for (int i=0; i<=n; i++)
        memo[i] = -1;

    return  getMinSteps(n, memo);
}

// driver program
int main()
{
    int n = 10;
    cout << getMinSteps(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to minimize n to 1
// by given rule in minimum steps
import java.io.*;
class GFG {

// function to calculate min steps
static int getMinSteps(int n, int memo[])
{
    // base case
    if (n == 1)
    return 0;
    if (memo[n] != -1)
    return memo[n];

    // store temp value for
    // n as min( f(n-1),
    // f(n/2), f(n/3)) +1
    int res = getMinSteps(n - 1, memo);

    if (n % 2 == 0)
        res = Math.min(res,
              getMinSteps(n / 2, memo));
    if (n % 3 == 0)
        res = Math.min(res,
               getMinSteps(n / 3, memo));

    // store memo[n] and return
    memo[n] = 1 + res;
    return memo[n];
}

// This function mainly
// initializes memo[] and
// calls getMinSteps(n, memo)
static int getMinSteps(int n)
{
    int memo[] = new int[n + 1];

    // initialize memoized array
    for (int i = 0; i <= n; i++)
        memo[i] = -1;

    return getMinSteps(n, memo);
}

    // Driver Code
    public static void main (String[] args)
    {
        int n = 10;
        System.out.println(getMinSteps(n));
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python program to minimize
# n to 1 by given
# rule in minimum steps

# function to calculate min steps
def getMinSteps(n, memo):

    # base case
    if (n == 1):
        return 0
    if (memo[n] != -1):
        return memo[n]

    # store temp value for n as min(f(n-1),
    # f(n//2), f(n//3)) + 1
    res = getMinSteps(n-1, memo)

    if (n%2 == 0):
        res = min(res, getMinSteps(n//2, memo))
    if (n%3 == 0):
        res = min(res, getMinSteps(n//3, memo))

    # store memo[n] and return
    memo[n] = 1 + res
    return memo[n]

# This function mainly
# initializes memo[] and
# calls getMinSteps(n, memo)
def getsMinSteps(n):

    memo = [0 for i in range(n+1)]

    # initialize memoized array
    for i in range(n+1):
        memo[i] = -1

    return getMinSteps(n, memo)

# driver program
n = 10
print(getsMinSteps(n))

# This code is contributed by Soumen Ghosh.  
```

## C#

```
// C# program to minimize n to 1
// by given rule in minimum steps
using System;

class GFG {

    // function to calculate min steps
    static int getMinSteps(int n, int []memo)
    {
        // base case
        if (n == 1)
            return 0;
        if (memo[n] != -1)
            return memo[n];

        // store temp value for
        // n as min( f(n-1),
        // f(n/2), f(n/3)) +1
        int res = getMinSteps(n - 1, memo);

        if (n % 2 == 0)
            res = Math.Min(res,
                getMinSteps(n / 2, memo));
        if (n % 3 == 0)
            res = Math.Min(res,
                getMinSteps(n / 3, memo));

        // store memo[n] and return
        memo[n] = 1 + res;

        return memo[n];
    }

    // This function mainly
    // initializes memo[] and
    // calls getMinSteps(n, memo)
    static int getMinSteps(int n)
    {
        int []memo = new int[n + 1];

        // initialize memoized array
        for (int i = 0; i <= n; i++)
            memo[i] = -1;

        return getMinSteps(n, memo);
    }

    // Driver Code
    public static void Main ()
    {
        int n = 10;
        Console.WriteLine(getMinSteps(n));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to minimize n to 1 by
// given rule in minimum steps

// function to calculate min steps
function getMinSteps( $n, $memo)
{

    // base case
    if ($n == 1)
        return 0;

    if ($memo[$n] != -1)
        return $memo[$n];

    // store temp value for n
    // as min( f(n-1),
    // f(n/2), f(n/3)) +1
    $res = getMinSteps($n - 1, $memo);

    if ($n % 2 == 0)
        $res = min($res, getMinSteps($n / 2, $memo));
    if ($n % 3 == 0)
        $res = min($res, getMinSteps($n / 3, $memo));

    // store memo[n] and return
    $memo[$n] = 1 + $res;
    return $memo[$n];
}

// This function mainly initializes
// memo[] and calls getMinSteps(n, memo)
function g_etMinSteps( $n)
{
    $memo= array();

    // initialize memoized array
    for($i = 0; $i <= $n; $i++)
        $memo[$i] = -1;

    return getMinSteps($n, $memo);
}

    // Driver Code
    $n = 10;
    echo g_etMinSteps($n);

// This code is contributed by anuj_67.
?>
```

**Output**

```
3
```

时间复杂度:O(n)，因为将有 n 个唯一的调用。

空间复杂度:0(n)

**下面是** [**制表**](https://www.geeksforgeeks.org/tabulation-vs-memoizatation/) **基础解:**

## C++

```
#include <bits/stdc++.h>
using namespace std;

int getMinSteps(int n)
{
    int table[n+1];
    table[1]=0;
    for (int i=2; i<=n; i++)
    {
    if (!(i%2) && (i%3))
        table[i] = 1+min(table[i-1], table[i/2]);
    else if (!(i%3) && (i%2))
        table[i] = 1+min(table[i-1], table[i/3]);
    else if(!(i%2) && !(i%3))
        table[i] = 1+min(table[i-1],min(table[i/2],table[i/3]));
    else
        table[i] =1+table[i-1];
    }
    return table[n];
}

// driver program
int main()
{
    int n = 14;
    cout << getMinSteps(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A tabulation based
// solution in Java
import java.io.*;

class GFG {
    static int getMinSteps(int n)
    {
        int[] dp = new int[n + 1];

        dp[1] = 0;

        for (int i = 2; i <= n; i++) {
            int min = dp[i - 1];

            if (i % 2 == 0) {
                min = Math.min(min, dp[i / 2]);
            }
            if (i % 3 == 0) {
                min = Math.min(min, dp[i / 3]);
            }
            dp[i] = min + 1;
        }

        return dp[n];
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 14;
        System.out.print(getMinSteps(n));
    }
}

// This code is contributed
// by anmol_sharma.
```

## 蟒蛇 3

```
# A tabulation based solution in Python3

def getMinSteps(n) :

    table = [0] * (n + 1)

    for i in range(n + 1) :
        table[i] = n-i

    for i in range(n, 0, -1) :

        if (not(i%2)) :
            table[i//2] = min(table[i]+1, table[i//2])

        if (not(i%3)) :
            table[i//3] = min(table[i]+1, table[i//3])

    return table[1]

# driver program
if __name__ == "__main__" :

    n = 14
    print(getMinSteps(n))

# This code is contributed by Ryuga
```

## C#

```
// A tabulation based
// solution in C#
using System;

class GFG
{
static int getMinSteps(int n)
{
    int []table = new int[n + 1];
    for (int i = 0; i <= n; i++)
        table[i] = n - i;
    for (int i = n; i >= 1; i--)
    {
    if (!(i % 2 > 0))
        table[i / 2] = Math.Min(table[i] + 1,
                                table[i / 2]);
    if (!(i % 3 > 0))
        table[i / 3] = Math.Min(table[i] + 1,
                                table[i / 3]);
    }
    return table[1];
}

// Driver Code
public static void Main ()
{
    int n = 10;
    Console.WriteLine(getMinSteps(n));
}
}

// This code is contributed
// by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A tabulation based solution in PHP

function getMinSteps( $n)
{
    $table = array();
    for ($i = 0; $i <= $n; $i++)
        $table[$i] = $n - $i;
    for ($i = $n; $i >= 1; $i--)
    {
        if (!($i % 2))
            $table[$i / 2] = min($table[$i] +
                          1, $table[$i / 2]);
        if (!($i % 3))
            $table[$i / 3] = min($table[$i] +
                          1, $table[$i / 3]);
    }
    return $table[1];
}

    // Driver Code
    $n = 10;
    echo getMinSteps($n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

    // A tabulation based solution in Javascript

    function getMinSteps(n)
    {
        let table = new Array(n+1);
        table.fill(0);
        table[1]=0;
        for (let i=2; i<=n; i++)
        {
          if (!(i%2) && (i%3))
              table[i] = 1+Math.min(table[i-1], table[i/2]);
          else if (!(i%3) && (i%2))
              table[i] = 1+Math.min(table[i-1], table[i/3]);
          else if(!(i%2) && !(i%3))
              table[i] = 1+Math.min(table[i-1],
              Math.min(table[i/2],table[i/3]));
          else
              table[i] =1+table[i-1];
        }
        return table[n] + 1;
    }

    let n = 10;
    document.write(getMinSteps(n));

</script>
```

**Output**

```
4
```

时间复杂度:O(n)，因为将有 n 个唯一的调用。

空间复杂度:0(n)

**使用递归:**

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
int getMinSteps(int n)
{
    // If n is equal to 1
    if (n == 1)
        return 0;

    int sub = INT_MAX;
    int div2 = INT_MAX;
    int div3 = INT_MAX;
    sub = getMinSteps(n - 1);

    if (n % 2 == 0)
        div2 = getMinSteps(n / 2);

    if (n % 3 == 0)
        div3 = getMinSteps(n / 3);

    return 1 + min(sub, min(div2, div3));
}

// Driver code
int main()
{
    int n = 10;

    // Function Call
    cout << (getMinSteps(n));

}

// This code is contributed by Potta Lokesh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above program
import java.io.*;

class GFG {
    public static int getMinSteps(int n)
    {
        // If n is equal to 1
        if (n == 1)
            return 0;

        int sub = Integer.MAX_VALUE;
        int div2 = Integer.MAX_VALUE;
        int div3 = Integer.MAX_VALUE;
        sub = getMinSteps(n - 1);

        if (n % 2 == 0)
            div2 = getMinSteps(n / 2);

        if (n % 3 == 0)
            div3 = getMinSteps(n / 3);

        return 1 + Math.min(sub, Math.min(div2, div3));
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 10;

        // Function Call
        System.out.print(getMinSteps(n));
    }
}
```

## C#

```
// C# program for the above program
using System;

class GFG
{
    public static int getMinSteps(int n)
    {

        // If n is equal to 1
        if (n == 1)
            return 0;

        int sub = Int32.MaxValue;
        int div2 = Int32.MaxValue;
        int div3 = Int32.MaxValue;
        sub = getMinSteps(n - 1);

        if (n % 2 == 0)
            div2 = getMinSteps(n / 2);

        if (n % 3 == 0)
            div3 = getMinSteps(n / 3);

        return 1 + Math.Min(sub, Math.Min(div2, div3));
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int n = 10;

        // Function Call
        Console.Write(getMinSteps(n));
    }
}

//This code is contributed by shivansinghss2110
```

## java 描述语言

```
<script>

    function getMinSteps(n)
    {
        // If n is equal to 1
        if (n == 1)
            return 0;

        let sub = Number.MAX_VALUE;
        let div2 = Number.MAX_VALUE;
        let div3 = Number.MAX_VALUE;
        sub = getMinSteps(n - 1);

        if (n % 2 == 0)
            div2 = getMinSteps(n / 2);

        if (n % 3 == 0)
            div3 = getMinSteps(n / 3);

        return 1 + Math.min(sub, Math.min(div2, div3));
    }

    let n = 10;

    // Function Call
    document.write(getMinSteps(n));

</script>
```

**Output**

```
3
```

时间复杂性:Exponential(O(2^n))

本文由[Shivam prad Han(anuj _ charm)](https://www.facebook.com/anuj.charm)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。