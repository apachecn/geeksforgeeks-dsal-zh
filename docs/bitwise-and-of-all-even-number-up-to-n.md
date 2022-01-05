# 所有偶数到 N 的按位“与”

> 原文:[https://www . geeksforgeeks . org/所有偶数的逐位和-up-n/](https://www.geeksforgeeks.org/bitwise-and-of-all-even-number-up-to-n/)

给定一个整数 **N** ，任务是找到从 1 到 N 的所有偶数的按位 and ( &)

**示例:**

> **输入:**2
> T3】输出: 2
> 
> **输入:** 10
> **输出:** 0
> **解释:**2、4、6、8、10 的位与为 0。

**天真方法:**将结果初始化为 2。从 4 到 n 迭代循环(对于所有偶数)并通过按位“与”(&)更新结果。
以下是实施办法:

## C++

```
// C++ implementation of the above approach
#include <iostream>
using namespace std;

// Function to return the bitwise &
// of all the even numbers upto N
int bitwiseAndTillN(int n)
{
    // Initialize result as 2
    int result = 2;

    for (int i = 4; i <= n; i = i + 2) {
        result = result & i;
    }
    return result;
}

// Driver code
int main()
{
    int n = 2;
    cout << bitwiseAndTillN(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

    // Function to return the bitwise &
    // of all the even numbers upto N
    static int bitwiseAndTillN(int n)
    {
        // Initialize result as 2
        int result = 2;

        for (int i = 4; i <= n; i = i + 2)
        {
            result = result & i;
        }
        return result;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 2;
        System.out.println(bitwiseAndTillN(n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to return the bitwise &
# of all the even numbers upto N
def bitwiseAndTillN(n) :

    # Initialize result as 2
    result = 2;

    for i in range(4, n + 1, 2) :
        result = result & i;

    return result;

# Driver code
if __name__ == "__main__" :

    n = 2;
    print(bitwiseAndTillN(n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to return the bitwise &
    // of all the even numbers upto N
    static int bitwiseAndTillN(int n)
    {
        // Initialize result as 2
        int result = 2;

        for (int i = 4; i <= n; i = i + 2)
        {
            result = result & i;
        }
        return result;
    }

    // Driver code
    public static void Main()
    {
        int n = 2;
        Console.WriteLine(bitwiseAndTillN(n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

// Function to return the bitwise &
// of all the even numbers upto N
function bitwiseAndTillN(n) {
    // Initialize result as 2
    let result = 2;

    for (let i = 4; i <= n; i = i + 2) {
        result = result & i;
    }
    return result;
}

// Driver code

let n = 2;
document.write(bitwiseAndTillN(n));
</script>
```

**Output:** 

```
2
```

**高效方式:**高效方式是 N 小于 4 返回 2，N 全部返回 0>= 4，因为 2 和 4 的按位 and 为 0，0 与任意数字的按位 and 为 0。
以下是实施办法:

## C++

```
// C++ implementation of the above approach
#include <iostream>
using namespace std;

// Function to return the bitwise &
// of all the numbers upto N
int bitwiseAndTillN(int n)
{
    if (n < 4)
        return 2;
    else
        return 0;
}

int main()
{
    int n = 2;
    cout << bitwiseAndTillN(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

    // Function to return the bitwise &
    // of all the numbers upto N
    static int bitwiseAndTillN(int n)
    {
        if (n < 4)
            return 2;
        else
            return 0;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 2;
        System.out.println(bitwiseAndTillN(n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to return the bitwise &
# of all the numbers upto N
def bitwiseAndTillN( n):
    if (n < 4):
        return 2
    else:
        return 0

# Driver code
n = 2
print(bitwiseAndTillN(n))

# This code is contributed by ANKITKUMAR34
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to return the bitwise &
    // of all the numbers upto N
    static int bitwiseAndTillN(int n)
    {
        if (n < 4)
            return 2;
        else
            return 0;
    }

    // Driver code
    public static void Main()
    {
        int n = 2;
        Console.WriteLine(bitwiseAndTillN(n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Function to return the bitwise &
// of all the numbers upto N
function bitwiseAndTillN(n)
{
    if (n < 4)
        return 2;
    else
        return 0;
}

// driver code

    let n = 2;
    document.write (bitwiseAndTillN(n));

 // this code is contributed by shivanisinghss2110 

</script>
```

**Output:** 

```
2
```