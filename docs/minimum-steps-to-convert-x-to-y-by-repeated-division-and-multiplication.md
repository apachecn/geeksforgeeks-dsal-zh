# 通过重复除法和乘法将 X 转换为 Y 的最少步骤

> 原文:[https://www . geesforgeks . org/通过重复除法和乘法将 x 转换为 y 的最小步骤/](https://www.geeksforgeeks.org/minimum-steps-to-convert-x-to-y-by-repeated-division-and-multiplication/)

给定两个整数 **X** 和 **Y** ，任务是使用每一步中的任何操作找到将整数 X 转换为 Y 的最小步数:

*   用任何自然数除这个数
*   将该数乘以任意自然数

**示例:**

> **输入:** X = 8，Y = 12
> **输出:** 2
> **解释:**
> 先将 8 除以 2: 8/2 = 4
> 再乘以 3: 4*3 = 12
> 
> **输入:** X = 4，Y = 8
> **输出:** 1
> **解释:**
> 将 4 转换为 8 将 4 乘以 2: 4 * 2 = 8

**方法:**解决上述问题:

*   确保 X 包含 X 和 Y 中较小的值。现在，**如果 X 大于 Y** ，那么我们知道将较小的数字更改为较大的数字总是更容易。因此，我们只需交换 X 和 Y 的值，然后按照下面提到的步骤操作。
*   **如果两个整数相同**，则答案为零，因为没有转换发生。
    例如 T3

```
If X = 4, Y = 4

Here 4 = 4
Therefore, answer = 0
(as they both are already same)
```

*   但是，**如果 X 小于 Y** ，那么:
    *   我们必须检查 Y % X 是否给出 0。
    *   如果是，那么 Y 可以表示为 **X * (Y / X)** ，我们单步得到想要的输出。
        例如 T3

```
If X = 4, Y = 12

Here 12 % 4 = 0
Therefore, answer = 1
(4 * 3 = 12)
```

*   否则，答案将是 2，因为它需要两步，一步用于除法(X = X/X)，另一步用于乘法(X = X * Y)。
    **例如**

```
If X = 8, Y = 13

Here 13 % 8 != 0
Therefore, 
1\. X = X/X = 8/8 = 1
2\. X = X*Y = 1*13 = 13

Hence, answer = 2
```

下面是上述方法的实现:

## C++

```
// C++ implementation to find minimum
// steps to convert X to Y by repeated
// division and multiplication

#include <bits/stdc++.h>
using namespace std;

int solve(int X, int Y)
{
    // Check if X is greater than Y
    // then swap the elements
    if (X > Y) {
        int temp = X;
        X = Y;
        Y = temp;
    }

    // Check if X equals Y
    if (X == Y)
        cout << 0 << endl;

    else if (Y % X == 0)
        cout << 1 << endl;
    else
        cout << 2 << endl;
}

// Driver code
int main()
{
    int X = 8, Y = 13;
    solve(X, Y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find minimum
// steps to convert X to Y by repeated
// division and multiplication
class GFG{

static int solve(int X, int Y)
{
    // Check if X is greater than Y
    // then swap the elements
    if (X > Y)
    {
        int temp = X;
        X = Y;
        Y = temp;
    }

    // Check if X equals Y
    if (X == Y)
        System.out.println(0 );

    else if (Y % X == 0)
        System.out.println( 1 );
    else
        System.out.println(2 );
        return 0;
}

// Driver code
public static void main(String args[])
{
    int X = 8, Y = 13;
    solve(X, Y);
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python3 implementation to find minimum
# steps to convert X to Y by repeated
# division and multiplication
def solve(X, Y):

    # Check if X is greater than Y
    # then swap the elements
    if (X > Y):
        temp = X
        X = Y
        Y = temp

    # Check if X equals Y
    if (X == Y):
        print(0)

    elif (Y % X == 0):
        print(1)
    else:
        print(2)

# Driver code
X = 8
Y = 13

solve(X, Y)

# This code is contributed by code_hunt
```

## C#

```
// C# implementation to find minimum
// steps to convert X to Y by repeated
// division and multiplication
using System;

class GFG{

static int solve(int X, int Y)
{

    // Check if X is greater than Y
    // then swap the elements
    if (X > Y)
    {
        int temp = X;
        X = Y;
        Y = temp;
    }

    // Check if X equals Y
    if (X == Y)
        Console.WriteLine(0);

    else if (Y % X == 0)
        Console.WriteLine(1);
    else
        Console.WriteLine(2);
    return 0;
}

// Driver code
public static void Main(String[] args)
{
    int X = 8, Y = 13;
    solve(X, Y);
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

    // Javascript implementation to find minimum
    // steps to convert X to Y by repeated
    // division and multiplication

    function solve(X, Y)
    {
        // Check if X is greater than Y
        // then swap the elements
        if (X > Y) {
            let temp = X;
            X = Y;
            Y = temp;
        }

        // Check if X equals Y
        if (X == Y)
            document.write(0);

        else if (Y % X == 0)
            document.write(1);
        else
            document.write(2);
    }

    let X = 8, Y = 13;
    solve(X, Y);

</script>
```

**Output:** 

```
2
```