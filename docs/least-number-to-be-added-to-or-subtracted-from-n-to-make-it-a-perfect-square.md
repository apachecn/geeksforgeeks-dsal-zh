# 最少要加或减的数，使其成为一个完美的正方形

> 原文:[https://www . geesforgeks . org/n 加或减最小数使其成为完美的正方形/](https://www.geeksforgeeks.org/least-number-to-be-added-to-or-subtracted-from-n-to-make-it-a-perfect-square/)

给定一个数 **N** ，求 **N** 需要加减的最小数，使其成为[完美正方形](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)。如果要加数字，用+号打印，否则如果要减数字，用–号打印。

**示例:**

> **输入:** N = 14
> **输出:**2
> 14 = 9
> 14 = 16
> 后最近的完美方块因此，需要将 2 加到 14 上才能得到最近的完美方块。
> 
> **输入:** N = 18
> **输出:**-2
> 18 = 16
> 18 = 25
> 后最近的完美正方形因此，需要从 18 中减去 2 才能得到最近的完美正方形。

**接近**:

1.  拿到号码。
2.  求数字的[平方根，将结果转换为整数。](https://www.geeksforgeeks.org/square-root-of-an-integer/)
3.  将双精度值转换为整数后，将包含 N 以上完美平方的根，即**楼(平方根(N))** 。
4.  然后求这个数的平方，这将是 n 之前的完美平方。
5.  求 N 后完美平方的根，即**天花板(平方根(N))** 。
6.  然后求这个数的平方，这将是 n 之后的完美平方。
7.  检查楼层值的平方是最接近 N 还是天花板值。
8.  如果楼层值的平方最接近 N，用-号打印差值。否则，用+号打印天花板值的平方和 N 之间的差值。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the Least number
int nearest(int n)
{

    // Get the perfect square
    // before and after N
    int prevSquare = sqrt(n);
    int nextSquare = prevSquare + 1;
    prevSquare = prevSquare * prevSquare;
    nextSquare = nextSquare * nextSquare;

    // Check which is nearest to N
    int ans
        = (n - prevSquare) < (nextSquare - n)
              ? (prevSquare - n)
              : (nextSquare - n);

    // return the result
    return ans;
}

// Driver code
int main()
{
    int n = 14;
    cout << nearest(n) << endl;

    n = 16;
    cout << nearest(n) << endl;

    n = 18;
    cout << nearest(n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the Least number
    static int nearest(int n)
    {

        // Get the perfect square
        // before and after N
        int prevSquare = (int)Math.sqrt(n);
        int nextSquare = prevSquare + 1;
        prevSquare = prevSquare * prevSquare;
        nextSquare = nextSquare * nextSquare;

        // Check which is nearest to N
        int ans = (n - prevSquare) < (nextSquare - n)? (prevSquare - n): (nextSquare - n);

        // return the result
        return ans;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 14;
        System.out.println(nearest(n));

        n = 16;
        System.out.println(nearest(n)) ;

        n = 18;
        System.out.println(nearest(n)) ;

    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import sqrt

# Function to return the Least number
def nearest(n) :

    # Get the perfect square
    # before and after N
    prevSquare = int(sqrt(n));
    nextSquare = prevSquare + 1;
    prevSquare = prevSquare * prevSquare;
    nextSquare = nextSquare * nextSquare;

    # Check which is nearest to N
    ans    = (prevSquare - n) if (n - prevSquare) < (nextSquare - n) else (nextSquare - n);

    # return the result
    return ans;

# Driver code
if __name__ == "__main__" :

    n = 14;
    print(nearest(n)) ;

    n = 16;
    print(nearest(n));

    n = 18;
    print(nearest(n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG {

    // Function to return the Least number
    static int nearest(int n)
    {

        // Get the perfect square
        // before and after N
        int prevSquare = (int)Math.Sqrt(n);
        int nextSquare = prevSquare + 1;
        prevSquare = prevSquare * prevSquare;
        nextSquare = nextSquare * nextSquare;

        // Check which is nearest to N
        int ans = (n - prevSquare) < (nextSquare - n)? (prevSquare - n): (nextSquare - n);

        // return the result
        return ans;
    }

    // Driver code
    public static void Main (string[] args)
    {
        int n = 14;
        Console.WriteLine(nearest(n));

        n = 16;
        Console.WriteLine(nearest(n)) ;

        n = 18;
        Console.WriteLine(nearest(n)) ;

    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

// Function to return the Least number
function nearest( n)
{
    // Get the perfect square
    // before and after N
    var prevSquare = parseInt(Math.sqrt(n));
    var nextSquare = prevSquare + 1;
    prevSquare = prevSquare * prevSquare;
    nextSquare = nextSquare * nextSquare;

    // Check which is nearest to N
     if((n - prevSquare) < (nextSquare - n))
     {
       ans = parseInt((prevSquare - n));
     }
     else
       ans = parseInt((nextSquare - n));

    // return the result
    return ans;
}

var  n = 14;
document.write( nearest(n) + "<br>");

n = 16;
document.write(  nearest(n)  + "<br>");

n = 18;
document.write(  nearest(n)  + "<br>");

// This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
2
0
-2
```