# 从 1 到 N 的所有奇数的按位“与”

> 原文:[https://www . geeksforgeeks . org/从 1 到 n 的所有奇数的逐位和/](https://www.geeksforgeeks.org/bitwise-and-of-all-the-odd-numbers-from-1-to-n/)

给定一个整数 **N** ，任务是从范围**【1，N】**中找到所有奇数的位“与”(&)。

**示例:**

> **输入:** N = 7
> **输出:** 1
> (1 & 3 & 5 & 7) = 1
> 
> **输入:**N = 1
> T3】输出: 1

**天真的做法:**从 **1** 开始，对所有奇数 **≤ N** 进行逐位 AND 运算。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to return the bitwise AND
// of all the odd integers from
// the range [1, n]
int bitwiseAndOdd(int n)
{
    // Initialize result to 1
    int result = 1;

    // Starting from 3, bitwise AND
    // all the odd integers less
    // than or equal to n
    for (int i = 3; i <= n; i = i + 2) {
        result = (result & i);
    }
    return result;
}

// Driver code
int main()
{
    int n = 10;

    cout << bitwiseAndOdd(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the bitwise AND
    // of all the odd integers from
    // the range [1, n]
    static int bitwiseAndOdd(int n)
    {
        // Initialize result to 1
        int result = 1;

        // Starting from 3, bitwise AND
        // all the odd integers less
        // than or equal to n
        for (int i = 3; i <= n; i = i + 2)
        {
            result = (result & i);
        }
        return result;
    }

    // Driver code
    public static void main (String[] args)
    {

        int n = 10;

        System.out.println(bitwiseAndOdd(n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the bitwise AND
# of all the odd integers from
# the range [1, n]
def bitwiseAndOdd(n) :

    # Initialize result to 1
    result = 1;

    # Starting from 3, bitwise AND
    # all the odd integers less
    # than or equal to n
    for i in range(3, n + 1, 2) :
        result = (result & i);

    return result;

# Driver code
if __name__ == "__main__" :

    n = 10;

    print(bitwiseAndOdd(n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the bitwise AND
    // of all the odd integers from
    // the range [1, n]
    static int bitwiseAndOdd(int n)
    {
        // Initialize result to 1
        int result = 1;

        // Starting from 3, bitwise AND
        // all the odd integers less
        // than or equal to n
        for (int i = 3; i <= n; i = i + 2)
        {
            result = (result & i);
        }
        return result;
    }

    // Driver code
    public static void Main()
    {

        int n = 10;
        Console.WriteLine(bitwiseAndOdd(n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the bitwise AND
// of all the odd integers from
// the range [1, n]
function bitwiseAndOdd(n)
{

    // Initialize result to 1
    var result = 1;

    // Starting from 3, bitwise AND
    // all the odd integers less
    // than or equal to n
    for(var i = 3; i <= n; i = i + 2)
    {
        result = (result & i);
    }
    return result;
}

// Driver code
var n = 10;

document.write(bitwiseAndOdd(n));

// This code is contributed by noob2000

</script>
```

**Output:** 

```
1
```

***时间复杂度:** O(n)*

***辅助空间:** O(1)*

**有效方法:**如果整数的最低有效位为 1(在这种情况下是所有奇数)，则按位与 1 的“与”运算结果总是为 1。所以，所有情况下的结果都是 1。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to return the bitwise AND
// of all the odd integers from
// the range [1, n]
int bitwiseAndOdd(int n)
{
    return 1;
}

// Driver code
int main()
{
    int n = 10;

    cout << bitwiseAndOdd(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the bitwise AND
    // of all the odd integers from
    // the range [1, n]
    static int bitwiseAndOdd(int n)
    {
        return 1;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 10;

        System.out.println(bitwiseAndOdd(n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the bitwise AND
# of all the odd integers from
# the range [1, n]
def bitwiseAndOdd(n):
    return 1

# Driver code
n = 10
print(bitwiseAndOdd(n))

# This code is contributed by ApurvaRaj
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the bitwise AND
    // of all the odd integers from
    // the range [1, n]
    static int bitwiseAndOdd(int n)
    {
        return 1;
    }

    // Driver code
    public static void Main()
    {
        int n = 10;

        Console.WriteLine(bitwiseAndOdd(n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the bitwise AND
// of all the odd integers from
// the range [1, n]
function bitwiseAndOdd(n)
{
    return 1;
}

// Driver code
var n = 10;
document.write( bitwiseAndOdd(n));

//This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
1
```

***时间复杂度:** O(1)*

***辅助空间:** O(1)*