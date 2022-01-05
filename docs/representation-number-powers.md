# 一个数的其他幂的表示

> 原文:[https://www.geeksforgeeks.org/representation-number-powers/](https://www.geeksforgeeks.org/representation-number-powers/)

给定两个数 w 和 m，我们需要确定是否可以用 w 的幂来表示 m，数 w 的幂可以相加或相减得到 m，w 的每个幂只能用一次。
**例:**

```
Input : 3 7
Output : Yes
As 7 = 9 - 3 + 1 (3^2 - 3^1 + 3^0 )
so it is possible .

Input : 100 50
Output : No
As 50 is less than 100 so we can never
represent it in the powers of 100 .
```

这里我们必须用 w 的幂来表示 m，w 只使用一次，所以可以通过下面的等式来表示。
**c0+c1*w^1+c2*w^2+……= m ——(等式 1)**
其中每个 c0、c1、C2……或者是 **-1** (用于减去 w 的幂)、 **0** (不使用 w 的幂)、 **1** (用于加上 w 的幂)。
**=>c1*w^1+c2*w^2+……= m–c0**
**=>w(C1+c2*w^1+c3*w^2+……)= m–c0**
**=>C1+c2*w^1+c3*w^2+……=(m–c0)/w——现在，请注意等式 1 和等式 2——我们正试图重新解决同一个问题。所以我们要递归到 m > 0。要使这样的解存在，(m-ci)必须是 w 的倍数，其中 ci 是方程的系数。ci 可以是-1，0，1。因此，我们必须检查所有三种可能性**((m–1)% w = = 0)、((m + 1 ) % w == 0)和(m % w == 0)** 。如果不是，那么就不会有任何解决办法。** 

## C++

```
// CPP program to check if m can be represented
// as powers of w.
#include <bits/stdc++.h>
using namespace std;

bool asPowerSum(int w, int m)
{
    while (m) {
        if ((m - 1) % w == 0)
            m = (m - 1) / w;
       else if ((m + 1) % w == 0)
            m = (m + 1) / w;

        else if (m % w == 0)
            m = m / w;

        else
            break; // None of 3 worked.
    }

    // If m is not zero means, it can't be
    // represented in terms of powers of w.
    return (m == 0);
}

// Driver code
int main()
{
    int w = 3, m = 7;
    if (asPowerSum(w, m))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if m can
// be represented as powers of w.

class GFG
{
    static boolean asPowerSum(int w, int m)
    {
        while (m > 0)
        {
            if ((m - 1) % w == 0)
                m = (m - 1) / w;

            else if ((m + 1) % w == 0)
                m = (m + 1) / w;

            else if (m % w == 0)
                m = m / w;

            else
                break; // None of 3 worked.
        }

        // If m is not zero means, it can't be
        // represented in terms of powers of w.
        return (m == 0);
    }

    // Driver function
    public static void main (String[] args)
    {
        int w = 3, m = 7;
        if (asPowerSum(w, m))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to check if m can
# be represented as powers of w.
def asPowerSum(w, m):
    while (m > 0):
        if ((m - 1) % w == 0):
            m = (m - 1) / w;

        elif ((m + 1) % w == 0):
            m = (m + 1) / w;

        elif (m % w == 0):
            m = m / w;

        else:
            break; # None of 3 worked.

    # If m is not zero means, it can't be
    # represented in terms of powers of w.
    return (m == 0);

# Driver code
w = 3;
m = 7;
if (asPowerSum(w, m)):
    print("Yes");
else:
    print("No");

# This code is contributed by mits
```

## C#

```
// C# program to check if
// m can be represented
// as powers of w.
using System;

class GFG
{
    static bool asPowerSum(int w,
                           int m)
    {
        while (m > 0)
        {
            if ((m - 1) % w == 0)
                m = (m - 1) / w;

            else if ((m + 1) % w == 0)
                m = (m + 1) / w;

            else if (m % w == 0)
                m = m / w;

            else
                break; // None of 3 worked.
        }

        // If m is not zero means,
        // it can't be represented
        // in terms of powers of w.
        return (m == 0);
    }

    // Driver Code
    static public void Main ()
    {
        int w = 3, m = 7;
        if (asPowerSum(w, m))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed
// by akt_mit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if m can
// be represented as powers of w.

function asPowerSum($w, $m)
{
    while ($m)
    {
        if (($m - 1) % $w == 0)
            $m = ($m - 1) / $w;
    else if (($m + 1) % $w == 0)
            $m = ($m + 1) / $w;

        else if ($m % $w == 0)
            $m = $m / $w;

        else
            break; // None of 3 worked.
    }

    // If m is not zero means, it can't be
    // represented in terms of powers of w.
    return ($m == 0);
}

// Driver code
$w = 3;
$m = 7;
if (asPowerSum($w, $m))
    echo "Yes\n";
else
    echo "No\n";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to check if m can
// be represented as powers of w.

    function asPowerSum(w, m)
    {
        while (m > 0)
        {
            if ((m - 1) % w == 0)
                m = (m - 1) / w;

            else if ((m + 1) % w == 0)
                m = (m + 1) / w;

            else if (m % w == 0)
                m = m / w;

            else
                break; // None of 3 worked.
        }

        // If m is not zero means, it can't be
        // represented in terms of powers of w.
        return (m == 0);
    }

// Driver code

        let w = 3, m = 7;
        if (asPowerSum(w, m))
            document.write("Yes");
        else
            document.write("No");

      // This code is contributed by sanjoy_62.
</script>
```

**输出:**

```
Yes
```