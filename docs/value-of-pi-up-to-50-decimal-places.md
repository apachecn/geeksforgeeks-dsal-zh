# 小数点后 50 位的π值

> 原文:[https://www . geesforgeks . org/pi 值-最多 50 位小数/](https://www.geeksforgeeks.org/value-of-pi-up-to-50-decimal-places/)

给定一个数字 **N** (其中 N < = 50)，任务是找到π(**π**)到 **N** 小数位数的值。
**示例:**

> **输入:** N = 2
> **输出:** 3.14
> **输入:** N = 10
> **输出:** 3.1415926536

**进场:**

1.π的值使用 [acos()函数](https://www.geeksforgeeks.org/acos-function-in-c-stl/)计算，该函数返回一个介于**[-π，π]**之间的数值。

2.因为使用 **acos(0.0)** 将返回**2 *π**的值。因此要得到**π**的值:

```
double pi = 2*acos(0.0);
```

3.现在从上述方程得到的值估计为 **N** 十进制数:

```
printf("%.*lf\n", N, pi);
```

下面是上述方法的实现:

## C++

```
// C++ program to calculate the
// value of pi up to n decimal
// places
#include "bits/stdc++.h"
using namespace std;

// Function that prints the
// value of pi upto N
// decimal places
void printValueOfPi(int N)
{

    // Find value of pi upto
    // using acos() function
    double pi = 2 * acos(0.0);

    // Print value of pi upto
    // N decimal places
    printf("%.*lf\n", N, pi);
}

// Driver Code
int main()
{
    int N = 45;

    // Function that prints
    // the value of pi
    printValueOfPi(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate the
// value of pi up to n decimal places
class GFG {

    // Function that prints the
    // value of pi upto N
    // decimal places
    static void printValueOfPi(int N)
    {

        // Find value of pi upto
        // using acos() function
        double pi = 2 * Math.acos(0.0);

        // Print value of pi upto
        // N decimal places
        System.out.println(pi);
    }

    // Driver Code
    public static void main (String[] args)
    {
        int N = 4;

        // Function that prints
        // the value of pi
        printValueOfPi(N);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to calculate the
# value of pi up to n decimal places
from math import acos

# Function that prints the
# value of pi upto N
# decimal places
def printValueOfPi(N) :

    # Find value of pi upto
    # using acos() function
    b = '{:.' + str(N) + 'f}'
    pi= b.format(2 * acos(0.0))

    # Print value of pi upto
    # N decimal places
    print(pi);

# Driver Code
if __name__ == "__main__" :

    N = 43;

    # Function that prints
    # the value of pi
    printValueOfPi(N);

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to calculate the
// value of pi up to n decimal places
using System;

class GFG {

    // Function that prints the
    // value of pi upto N
    // decimal places
    static void printValueOfPi(int N)
    {

        // Find value of pi upto
        // using acos() function
        double pi = 2 * Math.Acos(0.0);

        // Print value of pi upto
        // N decimal places
        Console.WriteLine(pi);
    }

    // Driver Code
    public static void Main()
    {
        int N = 4;

        // Function that prints
        // the value of pi
        printValueOfPi(N);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
    // Javascript program to calculate the
    // value of pi up to n decimal places

    // Function that prints the
    // value of pi upto N
    // decimal places
    function printValueOfPi(N)
    {

        // Find value of pi upto
        // using acos() function
        let pi = 2 * Math.acos(0.0);

        // Print value of pi upto
        // N decimal places
        document.write(pi.toFixed(4));
    }

    let N = 4;

    // Function that prints
    // the value of pi
    printValueOfPi(N);

// This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
3.1416
```

**时间复杂度:** O(1)