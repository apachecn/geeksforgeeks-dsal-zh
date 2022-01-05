# 不溶物编号

> 原文:[https://www.geeksforgeeks.org/insolite-numbers/](https://www.geeksforgeeks.org/insolite-numbers/)

**不可分解数**是一个数 **N** ，如果它可以被**和**整除，也可以被其数字平方的**乘积**整除。
极少不溶物编号为:

> 111、11112、1122112、111111111、122121216、11111112112……

### 检查一个号码是否为不可溶号码

给定一个数字 **N** ，任务是检查 **N** 是否为**曝光量数字**。如果 **N** 是不溶物号，则打印**“是”**否则打印**“否”**。
**示例:**

> **输入:** N = 1122112
> **输出:** Yes
> **解释:**
> 1122112 是一个**不可分解数**，因为
> 其位数的平方和 1^2+1^2+2^2+2^2+1^2+1^2+2^2 = 16
> 其位数的平方和(1*1*2*2*1*1*2)^2 = 64
> 和 1122112 可同时被 16 和 66 整除
> **输入:** N = 11
> **输出:**否
> T21【解释:

**方法:**不溶物数是一个数 **N** 如果它能被其数字的平方和和乘积整除。所以我们会找到 N 位数的平方和，N 位数的平方和的乘积，然后检查 N 是否能被和和乘积整除。如果可分，则打印**“是”**否则打印**“否”**。
以下是上述方法的实施:

## C++

```
// C++ implementation for the
// above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if a number
// is an Insolite numbers
bool isInsolite(int n)
{
    int N = n;

    // To store sum of squares of digits
    int sum = 0;

    // To store product of
    // squares of digits
    int product = 1;

    while (n != 0) {
        // extracting digit
        int r = n % 10;
        sum = sum + r * r;
        product = product * r * r;
        n = n / 10;
    }

    return (N % sum == 0)
           && (N % product == 0);
}

// Driver Code
int main()
{
    int N = 111;

    // Function Call
    if (isInsolite(N))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the
// above approach
class GFG{

// Function to check if a number
// is an Insolite numbers
static boolean isInsolite(int n)
{
    int N = n;

    // To store sum of squares of digits
    int sum = 0;

    // To store product of
    // squares of digits
    int product = 1;

    while (n != 0)
    {

        // extracting digit
        int r = n % 10;
        sum = sum + r * r;
        product = product * r * r;
        n = n / 10;
    }

    return (N % sum == 0) &&
           (N % product == 0);
}

// Driver Code
public static void main (String[] args)
{
    int N = 111;

    // Function Call
    if (isInsolite(N))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by rock_cool
```

## 蟒蛇 3

```
# Python3 implementation for the
# above approach

# Function to check if a number
# is an Insolite numbers
def isInsolite(n):
    N = n;

    # To store sum of squares of digits
    sum = 0;

    # To store product of
    # squares of digits
    product = 1;

    while (n != 0):

        # extracting digit
        r = n % 10;
        sum = sum + r * r;
        product = product * r * r;
        n = n // 10;

    return ((N % sum == 0) and
            (N % product == 0));

# Driver Code
if __name__ == '__main__':
    N = 111;

    # Function Call
    if (isInsolite(N)):
        print("Yes");
    else:
        print("No");

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation for the
// above approach
using System;
class GFG{

// Function to check if a number
// is an Insolite numbers
static bool isInsolite(int n)
{
    int N = n;

    // To store sum of squares of digits
    int sum = 0;

    // To store product of
    // squares of digits
    int product = 1;

    while (n != 0)
    {

        // extracting digit
        int r = n % 10;
        sum = sum + r * r;
        product = product * r * r;
        n = n / 10;
    }

    return (N % sum == 0) &&
           (N % product == 0);
}

// Driver Code
public static void Main()
{
    int N = 111;

    // Function Call
    if (isInsolite(N))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript implementation for the
// above approach

    // Function to check if a number
    // is an Insolite numbers
    function isInsolite( n) {
        let N = n;

        // To store sum of squares of digits
        let sum = 0;

        // To store product of
        // squares of digits
        let product = 1;

        while (n != 0) {

            // extracting digit
            let r = n % 10;
            sum = sum + r * r;
            product = product * r * r;
            n = parseInt(n / 10);
        }

        return (N % sum == 0) && (N % product == 0);
    }

    // Driver Code

        let N = 111;

        // Function Call
        if (isInsolite(N))
            document.write("Yes");
        else
            document.write("No");

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:***O(n)*
T5】参考:[http://www.numbersaplenty.com/set/insolite_number/](http://www.numbersaplenty.com/set/insolite_number/)