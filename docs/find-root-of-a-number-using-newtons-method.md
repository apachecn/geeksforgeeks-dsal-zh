# 用牛顿法求一个数的根

> 原文:[https://www . geesforgeks . org/find-number-of-use-newtons-method/](https://www.geeksforgeeks.org/find-root-of-a-number-using-newtons-method/)

给定一个整数 **N** 和一个公差等级 **L** ，任务是使用[牛顿法](https://en.wikipedia.org/wiki/Newton%27s_method)求该数的平方根。
**举例:**

> **输入:** N = 16，L = 0.0001
> **输出:** 4
> 4 <sup>2</sup> = 16
> **输入:** N = 327，L = 0.00001
> **输出:** 18.0831

**牛顿法:**
设 **N** 为任意数，则 **N** 的平方根可由公式
给出

> 根= 0.5 * (X + (N / X))其中 X 是可以假设为 N 或 1 的任何猜测。

*   在上式中， **X** 是 **N** 的任意假定平方根，**根**是 **N** 的正确平方根。
*   公差极限是 **X** 与允许根之间的最大差值。

**方法:**可以按照以下步骤计算答案:

1.  将 **X** 分配给 **N** 本身。
2.  现在，开始一个循环，继续计算**根**，它肯定会向 **N** 的正确平方根移动。
3.  检查假设的 **X** 和计算的**根**之间的差异，如果还不在公差范围内，则更新**根**并继续。
4.  如果计算出的**根**在允许的公差范围内，则脱离循环。
5.  打印**根**。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the square root of
// a number using Newtons method
double squareRoot(double n, float l)
{
    // Assuming the sqrt of n as n only
    double x = n;

    // The closed guess will be stored in the root
    double root;

    // To count the number of iterations
    int count = 0;

    while (1) {
        count++;

        // Calculate more closed x
        root = 0.5 * (x + (n / x));

        // Check for closeness
        if (abs(root - x) < l)
            break;

        // Update root
        x = root;
    }

    return root;
}

// Driver code
int main()
{
    double n = 327;
    float l = 0.00001;

    cout << squareRoot(n, l);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the square root of
    // a number using Newtons method
    static double squareRoot(double n, double l)
    {
        // Assuming the sqrt of n as n only
        double x = n;

        // The closed guess will be stored in the root
        double root;

        // To count the number of iterations
        int count = 0;

        while (true)
        {
            count++;

            // Calculate more closed x
            root = 0.5 * (x + (n / x));

            // Check for closeness
            if (Math.abs(root - x) < l)
                break;

            // Update root
            x = root;
        }

        return root;
    }

    // Driver code
    public static void main (String[] args)
    {
        double n = 327;
        double l = 0.00001;

        System.out.println(squareRoot(n, l));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the square root of
# a number using Newtons method
def squareRoot(n, l) :

    # Assuming the sqrt of n as n only
    x = n

    # To count the number of iterations
    count = 0

    while (1) :
        count += 1

        # Calculate more closed x
        root = 0.5 * (x + (n / x))

        # Check for closeness
        if (abs(root - x) < l) :
            break

        # Update root
        x = root

    return root

# Driver code
if __name__ == "__main__" :

    n = 327
    l = 0.00001

    print(squareRoot(n, l))

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the square root of
    // a number using Newtons method
    static double squareRoot(double n, double l)
    {
        // Assuming the sqrt of n as n only
        double x = n;

        // The closed guess will be stored in the root
        double root;

        // To count the number of iterations
        int count = 0;

        while (true)
        {
            count++;

            // Calculate more closed x
            root = 0.5 * (x + (n / x));

            // Check for closeness
            if (Math.Abs(root - x) < l)
                break;

            // Update root
            x = root;
        }

        return root;
    }

    // Driver code
    public static void Main()
    {
        double n = 327;
        double l = 0.00001;

        Console.WriteLine(squareRoot(n, l));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the square root of
    // a number using Newtons method
    function squareRoot(n, l)
    {
        // Assuming the sqrt of n as n only
        let x = n;

        // The closed guess will be stored in the root
        let root;

        // To count the number of iterations
        let count = 0;

        while (true)
        {
            count++;

            // Calculate more closed x
            root = 0.5 * (x + (n / x));

            // Check for closeness
            if (Math.abs(root - x) < l)
                break;

            // Update root
            x = root;
        }

        return root.toFixed(4);
    }

    let n = 327;
    let l = 0.00001;

    document.write(squareRoot(n, l));

 // This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
18.0831
```