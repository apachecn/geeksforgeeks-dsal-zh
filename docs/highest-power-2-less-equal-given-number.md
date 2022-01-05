# 小于等于给定数的 2 的最高幂

> 原文:[https://www . geesforgeks . org/最高幂 2 减等给定数/](https://www.geeksforgeeks.org/highest-power-2-less-equal-given-number/)

给定一个数 n，求小于或等于 n 的 2 的最高幂。

**例:**

```
Input : n = 10
Output : 8

Input : n = 19
Output : 16

Input : n = 32
Output : 32
```

一个**简单的解决方案**是从 n 开始检查，一直递减，直到我们找到 2 的幂。

## c++

```
// C++ program to find highest power of 2 smaller
// than or equal to n.
#include<bits/stdc++.h>
using namespace std;

int highestPowerof2(int n)
{
    int res = 0;
    for (int i=n; i>=1; i--)
    {
        // If i is a power of 2
        if ((i & (i-1)) == 0)
        {
            res = i;
            break;
        }
    }
    return res;
}

// Driver code
int main()
{
    int n = 10;
    cout << highestPowerof2(n);
    return 0;
}
```

## Java

```
// Java program to find highest power of
// 2 smaller than or equal to n.
class GFG{

static int highestPowerof2(int n)
{
    int res = 0;
    for(int i = n; i >= 1; i--)
    {

        // If i is a power of 2
        if ((i & (i-1)) == 0)
        {
            res = i;
            break;
        }
    }
    return res;
}

// Driver code
public static void main(String[] args)
{
    int n = 10;

    System.out.print(highestPowerof2(n));
}
}

// This code is contributed by 29AjayKumar
```

## python 3

```
# Python3 program to find highest
# power of 2 smaller than or
# equal to n.
def highestPowerof2(n):

    res = 0;
    for i in range(n, 0, -1):

        # If i is a power of 2
        if ((i & (i - 1)) == 0):

            res = i;
            break;

    return res;

# Driver code
n = 10;
print(highestPowerof2(n));

# This code is contributed by mits
```

## c#

```
// C# code to find highest power
// of 2 smaller than or equal to n.
using System;

class GFG
{
public static int highestPowerof2(int n)
{
    int res = 0;
    for (int i = n; i >= 1; i--)
        {
        // If i is a power of 2
        if ((i & (i - 1)) == 0)
            {
                res = i;
                break;
            }
        }
    return res;
}

    // Driver Code
    static public void Main ()
    {
        int n = 10;
        Console.WriteLine(highestPowerof2(n));
    }
}

// This code is contributed by ajit
```

## PHP

```
<?php
// PHP program to find highest
// power of 2 smaller than or
// equal to n.
function highestPowerof2($n)
{
    $res = 0;
    for ($i = $n; $i >= 1; $i--)
    {
        // If i is a power of 2
        if (($i & ($i - 1)) == 0)
        {
            $res = $i;
            break;
        }
    }
    return $res;
}

// Driver code
$n = 10;
echo highestPowerof2($n);

// This code is contributed by m_kit
?>
```

## Javascript

```
<script>

// JavaScript program to find highest power
// of 2 smaller than or equal to n.

   function highestPowerof2(n)
   {
     let res = 0;
     for (let i = n; i >= 1; i--)
        {
         // If i is a power of 2
          if ((i & (i - 1)) == 0)
             {
                  res = i;
                break;
             }
        }
     return res;
   }

// Driver code
      let n = 10;
      document.write(highestPowerof2(n));

</script>
```

**输出**

```
8
```