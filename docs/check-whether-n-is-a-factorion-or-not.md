# 检查 N 是否为因子

> 原文:[https://www . geesforgeks . org/check-n-is-factor-or-not/](https://www.geeksforgeeks.org/check-whether-n-is-a-factorion-or-not/)

给定一个整数 **N** ，任务是检查 **N** 是否为[因子](https://en.wikipedia.org/wiki/Factorion)。因子是一个数，它等于其位数的因子之和。
**举例:**

> **输入:**N = 40585
> T3】输出:是
> 4！+ 0!+ 5!+ 8!+ 5!= 40585
> **输入:** N = 234
> **输出:**否
> 2！+ 3!+ 4!= 32

**方法:**创建一个大小为 **10** 的数组**fact【】**来存储所有可能数字的阶乘，其中**fact【I】**存储 **i！**。现在，对于给定数字的所有数字，使用前面计算的**事实[]** 数组，找到这些数字的阶乘之和。如果和等于给定的数，那么这个数就是一个因子，否则就不是。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define MAX 10

// Function that returns true
// if n is a Factorion
bool isFactorion(int n)
{

    // fact[i] will store i!
    int fact[MAX];
    fact[0] = 1;
    for (int i = 1; i < MAX; i++)
        fact[i] = i * fact[i - 1];

    // A copy of the given integer
    int org = n;

    // To store the sum of factorials
    // of the digits of n
    int sum = 0;
    while (n > 0) {

        // Get the last digit
        int d = n % 10;

        // Add the factorial of the current
        // digit to the sum
        sum += fact[d];

        // Remove the last digit
        n /= 10;
    }

    if (sum == org)
        return true;

    return false;
}

// Driver code
int main()
{
    int n = 40585;
    if (isFactorion(n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{
    static int MAX = 10;

    // Function that returns true
    // if n is a Factorion
    static boolean isFactorion(int n)
    {
        // fact[i] will store i!
        int fact[] = new int[MAX];

        fact[0] = 1;
        for (int i = 1; i < MAX; i++)
            fact[i] = i * fact[i - 1];

        // A copy of the given integer
        int org = n;

        // To store the sum of factorials
        // of the digits of n
        int sum = 0;
        while (n > 0)
        {

            // Get the last digit
            int d = n % 10;

            // Add the factorial of the current
            // digit to the sum
            sum += fact[d];

            // Remove the last digit
            n /= 10;
        }

        if (sum == org)
            return true;

        return false;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 40585;
        if (isFactorion(n))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach
MAX = 10

# Function that returns true
# if n is a Factorion
def isFactorion(n) :

    # fact[i] will store i!
    fact = [0] * MAX
    fact[0] = 1
    for i in range(1, MAX) :
        fact[i] = i * fact[i - 1]

    # A copy of the given integer
    org = n

    # To store the sum of factorials
    # of the digits of n
    sum = 0
    while (n > 0) :

        # Get the last digit
        d = n % 10

        # Add the factorial of the current
        # digit to the sum
        sum += fact[d]

        # Remove the last digit
        n = n // 10

    if (sum == org):
        return True

    return False

# Driver code
n = 40585

if (isFactorion(n)):
    print("Yes")
else:
    print("No")

# This code is contributed by
# divyamohan123
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
    static int MAX = 10;

    // Function that returns true
    // if n is a Factorion
    static bool isFactorion(int n)
    {
        // fact[i] will store i!
        int [] fact = new int[MAX];

        fact[0] = 1;
        for (int i = 1; i < MAX; i++)
            fact[i] = i * fact[i - 1];

        // A copy of the given integer
        int org = n;

        // To store the sum of factorials
        // of the digits of n
        int sum = 0;
        while (n > 0)
        {

            // Get the last digit
            int d = n % 10;

            // Add the factorial of the current
            // digit to the sum
            sum += fact[d];

            // Remove the last digit
            n /= 10;
        }

        if (sum == org)
            return true;

        return false;
    }

    // Driver code
    public static void Main (String[] args)
    {
        int n = 40585;
        if (isFactorion(n))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by Mohit kumar
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

const MAX = 10;

// Function that returns true
// if n is a Factorion
function isFactorion(n)
{

    // fact[i] will store i!
    let fact = new Array(MAX);
    fact[0] = 1;
    for (let i = 1; i < MAX; i++)
        fact[i] = i * fact[i - 1];

    // A copy of the given integer
    let org = n;

    // To store the sum of factorials
    // of the digits of n
    let sum = 0;
    while (n > 0) {

        // Get the last digit
        let d = n % 10;

        // Add the factorial of the current
        // digit to the sum
        sum += fact[d];

        // Remove the last digit
        n = parseInt(n / 10);
    }

    if (sum == org)
        return true;

    return false;
}

// Driver code
    let n = 40585;
    if (isFactorion(n))
        document.write("Yes");
    else
        document.write("No");

</script>
```

**Output:** 

```
Yes
```