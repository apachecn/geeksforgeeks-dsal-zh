# 前 N 个自然数差之和的两个可能集合为 D

> 原文:[https://www . geesforgeks . org/可能-从第一个 n 个自然数开始的两个集合-和差为-d/](https://www.geeksforgeeks.org/possible-two-sets-from-first-n-natural-numbers-difference-of-sums-as-d/)

给定 N 和 D，找出是否有可能由前 N 个自然数生成两个集合，使得两个集合之和(单独)之差为 D。
**示例:**

```
Input  : 5 7
Output : yes
Explanation: Keeping 1 and 3 in one set,
and 2, 4 and 5 are in other set.
Sum of set 1 = 4
Sum of set 2 = 11 
So, the difference D = 7 
Which is the required difference

Input  : 4 5
Output : no
```

**进场:**

> 设 s1 和 s2 为两组。
> 这里我们知道
> 和(s1) +和(s2) = N*(N+1)/2 和
> 和(s1)–和(s2) = D
> 把上面 2 个方程相加，我们得到
> 2 *和(s1) = N*(N+1)/2 + D
> 如果和(S1)和和(s2)都是整数，那么只有我们能把前 N 个自然数拆分成两组。为此，N*(N+1)/2 + D 必须是偶数。

## C++

```
// C++ program for implementing
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function returns true if it is
// possible to split into two
// sets otherwise returns false
bool check(int N, int D)
{   
    int temp = (N * (N + 1)) / 2 + D;
    return (temp % 2 == 0);
}

// Driver code
int main()
{
    int N = 5;
    int M = 7;
    if (check(N, M))
        cout << "yes";
    else
        cout << "no";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for implementing
// above approach

class GFG
{

    // Function returns true if it is
    // possible to split into two
    // sets otherwise returns false
    static boolean check(int N, int D)
    {
        int temp = (N * (N + 1)) / 2 + D;
        return (temp % 2 == 0);
    }

    // Driver code
    static public void main (String args[])
    {
        int N = 5;
        int M = 7;
        if (check(N, M))
            System.out.println("yes");
        else
            System.out.println("no");
    }
}

// This code is contributed by Smitha.
```

## 蟒蛇 3

```
# Python program for implementing
# above approach

# Function returns true if it is
# possible to split into two
# sets otherwise returns false
def check(N, D):
    temp = N * (N + 1) // 2 + D
    return (bool(temp % 2 == 0))

# Driver code
N = 5
M = 7
if check(N, M):
    print("yes")
else:
    print("no")

# This code is contributed by Shrikant13.
```

## C#

```
// C# program for implementing
// above approach
using System;

class GFG
{

    // Function returns true if it is
    // possible to split into two
    // sets otherwise returns false
    static bool check(int N, int D)
    {
        int temp = (N * (N + 1)) / 2 + D;
        return (temp % 2 == 0);
    }

    // Driver code
    static public void Main ()
    {
        int N = 5;
        int M = 7;
        if (check(N, M))
            Console.Write("yes");
        else
            Console.Write("no");
    }
}

// This code is contributed by Ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for implementing
// above approach

// Function returns true if it is
// possible to split into two
// sets otherwise returns false
function check($N, $D)
{
    $temp = ($N * ($N + 1)) / 2 + $D;
    return ($temp % 2 == 0);
}

// Driver code
$N = 5;
$M = 7;
if (check($N, $M))
    echo("yes");
else
    echo("no");

// This code is contributed by Ajit.
```

## java 描述语言

```
<script>

// javascript program for implementing
// above approach

// Function returns true if it is
// possible to split into two
// sets otherwise returns false
function check( N,  D)
{   
    let temp = (N * (N + 1)) / 2 + D;
    return (temp % 2 == 0);
}

// Driver code

    let N = 5;
    let M = 7;
    if (check(N, M))
       document.write( "yes");
    else
       document.write("no");

// This code contributed by aashish1995

</script>
```

**输出:**

```
yes
```