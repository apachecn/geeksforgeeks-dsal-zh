# 给定范围内偶数因子的元素数量

> 原文:[https://www . geeksforgeeks . org/给定范围内具有偶数因子的元素数量/](https://www.geeksforgeeks.org/number-of-elements-with-even-factors-in-the-given-range/)

给定一个范围[n，m]，任务是找出在给定范围(包括 n 和 m)内具有偶数个因子的元素的数量。
**例:**

```
Input: n = 5, m = 20
Output: 14
The numbers with even factors are 
5, 6, 7, 8, 10, 11, 12, 13, 14, 15, 17, 18, 19, 20.

Input: n = 5, m = 100
Output: 88
```

一个**简单的解决方法**是从 n 开始循环所有的数字，对于每个数字，检查它是否有偶数个因子。如果它有偶数个因子，那么增加这些数字的计数，最后打印这些元素的数量。要高效地找到一个自然数的所有除数，请参考[自然数的所有除数](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)
一个**高效的解决方案**是找到具有奇数因子的[数](https://www.geeksforgeeks.org/number-elements-odd-factors-given-range/)，即只有完美正方形具有奇数因子，因此除了完美正方形之外的所有数字都将具有偶数因子。所以，找出范围内完美方块的个数，从总数中减去，即 **m-n+1** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the perfect squares
int countOddSquares(int n, int m)
{
    return (int)pow(m, 0.5) - (int)pow(n - 1, 0.5);
}

// Driver code
int main()
{
    int n = 5, m = 100;
    cout << "Count is "
         << (m - n + 1) - countOddSquares(n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.io.*;

class GFG
{

// Function to count the perfect squares
static int countOddSquares(int n, int m)
{
    return (int)Math.pow(m, 0.5) -
            (int)Math.pow(n - 1, 0.5);
}

// Driver code
public static void main (String[] args)
{
    int n = 5, m = 100;
    System.out.println("Count is " + ((m - n + 1)
                    - countOddSquares(n, m)));
}
}

// This code is contributed by ajit..
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Function to count the perfect squares
def countOddSquares(n, m) :
    return (int(pow(m, 0.5)) -
            int(pow(n - 1, 0.5)))

# Driver code
if __name__ == "__main__" :

    n = 5 ; m = 100;
    print("Count is", (m - n + 1) -
                       countOddSquares(n, m))

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

// Function to count the perfect squares
static int countOddSquares(int n, int m)
{
    return (int)Math.Pow(m, 0.5) -
            (int)Math.Pow(n - 1, 0.5);
}

// Driver code
static public void Main ()
{
    int n = 5, m = 100;
    Console.WriteLine("Count is " + ((m - n + 1)
                    - countOddSquares(n, m)));
}
}

// This Code is contributed by akt_mit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the
// above approach

// Function to count the perfect squares
function countOddSquares($n, $m)
{
    return (int)pow($m, 0.5) -
           (int)pow($n - 1, 0.5);
}

// Driver code
$n = 5;
$m = 100;
echo "Count is ", ($m - $n + 1) -
                   countOddSquares($n, $m);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to count the perfect squares
function countOddSquares(n, m)
{
    return Math.pow(m,0.5) - Math.pow(n - 1, 0.5);
}

// Driver code
var n = 5, m = 100;
document.write( "Count is "
     + ((m - n + 1) - countOddSquares(n, m)));

</script>
```

**Output:** 

```
Count is 88
```