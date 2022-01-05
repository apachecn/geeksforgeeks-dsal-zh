# 从 N 中找出达到 M 的最小步数

> 原文:[https://www . geesforgeks . org/find-最小到达步数-m-from-n/](https://www.geeksforgeeks.org/find-the-minimum-number-of-steps-to-reach-m-from-n/)

给定两个整数 **N** 和 **M** 。任务是通过执行给定的操作，从 N 中找到达到 M 的最小步数。

1.  将数字 x 乘以 2。所以，x 变成了 2*x。
2.  从数字 x 中减去 1。所以，x 变成 x-1。

**例:**

```
Input : N = 4, M = 6
Output : 2
Explanation : Perform operation number 2 on N. 
So, N becomes 3 and then perform operation number 1\. 
Then, N becomes 6\. So, the minimum number of steps is 2\. 

Input : N = 10, M = 1
Output : 9
Explanation : Perform operation number two 
9 times on N. Then N becomes 1.
```

**逼近** :
思路是把问题反过来如下:我们应该用
运算得到从 M 开始的数 N

1.  如果这个数是偶数，就除以 2。
2.  在数字上加 1。

现在，最小操作次数将是:

1.  如果 N > M，返回它们之间的差值，即步数将加 1 到 M，直到等于 N
2.  否则，如果 N < M
    *   继续将 M 除以 2，直到它小于 n。如果 M 是奇数，先加 1，然后除以 2。一旦 M 小于 N，将它们之间的差值与上述操作的计数相加。

以下是上述方法的实现:

## C++

```
// CPP program to find minimum number
// of steps to reach M from N
#include <bits/stdc++.h>
using namespace std;

// Function to find a minimum number
// of steps to reach M from N
int Minsteps(int n, int m)
{
    int ans = 0;

    // Continue till m is greater than n
    while(m > n)
    {
        // If m is odd
        if(m&1)
        {
            // add one
            m++;
            ans++;
        }

        // divide m by 2       
        m /= 2;
        ans++;
    }

    // Return the required answer
    return ans + n - m;
}

// Driver code
int main()
{
    int n = 4, m = 6;

    cout << Minsteps(n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum number
// of steps to reach M from N
class CFG
{

// Function to find a minimum number
// of steps to reach M from N
static int Minsteps(int n, int m)
{
    int ans = 0;

    // Continue till m is greater than n
    while(m > n)
    {
        // If m is odd
        if(m % 2 != 0)
        {
            // add one
            m++;
            ans++;
        }

        // divide m by 2    
        m /= 2;
        ans++;
    }

    // Return the required answer
    return ans + n - m;
}

// Driver code
public static void main(String[] args)
{
    int n = 4, m = 6;

    System.out.println(Minsteps(n, m));
}
}

// This code is contributed by Code_Mech
```

## 蟒蛇 3

```
# Python3 program to find minimum number
# of steps to reach M from N

# Function to find a minimum number
# of steps to reach M from N
def Minsteps(n, m):

    ans = 0

    # Continue till m is greater than n
    while(m > n):

        # If m is odd
        if(m & 1):

            # add one
            m += 1
            ans += 1

        # divide m by 2    
        m //= 2
        ans += 1

    # Return the required answer
    return ans + n - m

# Driver code
n = 4
m = 6

print(Minsteps(n, m))

# This code is contributed by mohit kumar
```

## C#

```
// C# program to find minimum number
// of steps to reach M from N
using System;

class GFG
{

// Function to find a minimum number
// of steps to reach M from N
static int Minsteps(int n, int m)
{
    int ans = 0;

    // Continue till m is greater than n
    while(m > n)
    {
        // If m is odd
        if(m % 2 != 0)
        {
            // add one
            m++;
            ans++;
        }

        // divide m by 2    
        m /= 2;
        ans++;
    }

    // Return the required answer
    return ans + n - m;
}

// Driver code
public static void Main()
{
    int n = 4, m = 6;

    Console.WriteLine(Minsteps(n, m));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum number
// of steps to reach M from N

// Function to find a minimum number
// of steps to reach M from N
function Minsteps($n, $m)
{
    $ans = 0;

    // Continue till m is greater than n
    while($m > $n)
    {
        // If m is odd
        if($m % 2 != 0)
        {
            // add one
            $m++;
            $ans++;
        }

        // divide m by 2    
        $m /= 2;
        $ans++;
    }

    // Return the required answer
    return $ans + $n - $m;
}

// Driver code
$n = 4; $m = 6;

echo(Minsteps($n, $m));

// This code is contributed by Code_Mech
?>
```

## java 描述语言

```
<script>
// JavaScript program to find minimum number
// of steps to reach M from N

// Function to find a minimum number
// of steps to reach M from N
function Minsteps(n, m)
{
    let ans = 0;

    // Continue till m is greater than n
    while(m > n)
    {
        // If m is odd
        if(m&1)
        {
            // add one
            m++;
            ans++;
        }

        // divide m by 2       
        m = Math.floor(m / 2);
        ans++;
    }

    // Return the required answer
    return ans + n - m;
}

// Driver code
    let n = 4, m = 6;   
    document.write(Minsteps(n, m));

// This code is contributed by Surbhi Tyagi.
</script>
```

**Output:** 

```
2
```