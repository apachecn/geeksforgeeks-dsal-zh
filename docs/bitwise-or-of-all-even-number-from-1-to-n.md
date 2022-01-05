# 从 1 到 N 的所有偶数的位或(|)

> 原文:[https://www . geesforgeks . org/从 1 到 n 的所有偶数的按位或/](https://www.geeksforgeeks.org/bitwise-or-of-all-even-number-from-1-to-n/)

给定一个数字 **N** ，任务是找到从 1 到 N 的所有偶数的按位 OR( |)

**示例:**

> **输入:**2
> T3】输出: 2
> 
> **输入:** 10
> **输出:** 14
> **解释:** 2 | 4 | 6 | 8 | 10 = 14

**简单方法:**将结果初始化为 2。从 4 到 n 循环迭代(对于所有偶数)并通过按位“或”(|)更新结果。

以下是该方法的实施情况:

## C++

```
// C++ implementation of the above approach
#include <iostream>
using namespace std;

// Function to return the bitwise OR
// of all the even numbers upto N
int bitwiseOrTillN(int n)
{
    // Initialize result as 2
    int result = 2;

    for (int i = 4; i <= n; i = i + 2) {
        result = result | i;
    }
    return result;
}

// Driver code
int main()
{
    int n = 10;
    cout << bitwiseOrTillN(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

    // Function to return the bitwise OR
    // of all the even numbers upto N
    static int bitwiseOrTillN(int n)
    {
        // Initialize result as 2
        int result = 2;

        for (int i = 4; i <= n; i = i + 2)
        {
            result = result | i;
        }
        return result;
    }

    // Driver code
    static public void main (String args[])
    {
        int n = 10;
        System.out.println(bitwiseOrTillN(n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python 3 implementation of the above approach

# Function to return the bitwise OR
# of all the even numbers upto N
def bitwiseOrTillN ( n ):

    # Initialize result as 2
    result = 2;

    for i in range(4, n + 1, 2) :
        result = result | i

    return result

# Driver code
n = 10;
print(bitwiseOrTillN(n));

# This code is contributed by ANKITKUMAR34
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to return the bitwise OR
    // of all the even numbers upto N
    static int bitwiseOrTillN(int n)
    {
        // Initialize result as 2
        int result = 2;

        for (int i = 4; i <= n; i = i + 2)
        {
            result = result | i;
        }
        return result;
    }

    // Driver code
    static public void Main ()
    {
        int n = 10;
        Console.WriteLine(bitwiseOrTillN(n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to return the bitwise OR
// of all the even numbers upto N
function bitwiseOrTillN(n)
{

    // Initialize result as 2
    var result = 2;

    for(var i = 4; i <= n; i = i + 2)
    {
        result = result | i;
    }
    return result;
}

// Driver code
var n = 10;
document.write( bitwiseOrTillN(n));

// This code is contributed by noob2000

</script>
```

**Output:** 

```
14
```

**有效方法:**计算 **N** 中的总位数。在按位“或”运算中，最右边的位将为 0，所有其他位将为 1。因此，返回功率(2，总位数)-2。它将给出按位“或”的十进制等值。

以下是该方法的实施情况:

## C++

```
// C++ implementation of the above approach
#include <iostream>
#include <math.h>
using namespace std;

// Function to return the bitwise OR
// of all even numbers upto N
int bitwiseOrTillN(int n)
{
    // For value less than 2
    if (n < 2)
        return 0;

    // Count total number of bits in bitwise or
    // all bits will be set except last bit
    int bitCount = log2(n) + 1;

    // Compute 2 to the power bitCount and subtract 2
    return pow(2, bitCount) - 2;
}

// Driver code
int main()
{
    int n = 10;
    cout << bitwiseOrTillN(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

    // Function to return the bitwise OR
    // of all even numbers upto N
    static int bitwiseOrTillN(int n)
    {
        // For value less than 2
        if (n < 2)
            return 0;

        // Count total number of bits in bitwise or
        // all bits will be set except last bit
        int bitCount = (int)(Math.log(n)/Math.log(2)) + 1;

        // Compute 2 to the power bitCount and subtract 2
        return (int)Math.pow(2, bitCount) - 2;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 10;
        System.out.println(bitwiseOrTillN(n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
from math import log2

# Function to return the bitwise OR
# of all even numbers upto N
def bitwiseOrTillN(n) :

    # For value less than 2
    if (n < 2) :
        return 0;

    # Count total number of bits in bitwise or
    # all bits will be set except last bit
    bitCount = int(log2(n)) + 1;

    # Compute 2 to the power bitCount and subtract 2
    return pow(2, bitCount) - 2;

# Driver code
if __name__ == "__main__" :

    n = 10;
    print(bitwiseOrTillN(n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to return the bitwise OR
    // of all even numbers upto N
    static int bitwiseOrTillN(int n)
    {
        // For value less than 2
        if (n < 2)
            return 0;

        // Count total number of bits in bitwise or
        // all bits will be set except last bit
        int bitCount = (int)(Math.Log(n)/Math.Log(2)) + 1;

        // Compute 2 to the power bitCount and subtract 2
        return (int)Math.Pow(2, bitCount) - 2;
    }

    // Driver code
    public static void Main()
    {
        int n = 10;
        Console.WriteLine(bitwiseOrTillN(n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the bitwise OR
// of all even numbers upto N
function bitwiseOrTillN(n)
{
    // For value less than 2
    if (n < 2)
        return 0;

    // Count total number of bits in bitwise or
    // all bits will be set except last bit
    var bitCount = parseInt(Math.log2(n) + 1);

    // Compute 2 to the power bitCount and subtract 2
    return Math.pow(2, bitCount) - 2;
}

// Driver code
var n = 10;
document.write(  bitwiseOrTillN(n));

//This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
14
```