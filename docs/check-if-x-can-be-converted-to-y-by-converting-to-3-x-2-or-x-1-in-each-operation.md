# 通过在每次操作中转换为 3 * (X / 2)或 X–1 来检查 X 是否可以转换为 Y

> 原文:[https://www . geesforgeks . org/check-if-x-can-converting-to-3-x-2-or-x-1-in-one-operation/](https://www.geeksforgeeks.org/check-if-x-can-be-converted-to-y-by-converting-to-3-x-2-or-x-1-in-each-operation/)

给定两个正整数 **X** 和 **Y** ，任务是通过反复将 **X** 的值更改为 **(3 * X / 2)** ( *如果 **X** 为偶数*)或**(X–1)**)来检查 **X** 是否可以转换为 **Y** 。如果可以将 **X** 转换为 **Y** ，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** X = 6，Y = 8
> **输出:**是
> **解释:**
> **操作 1:** 将 X(= 6)转换为 3*X/2 ( = 3 * (6 / 2) = 9)。
> **操作 2:** 将 X(= 9)转换为(X–1)(= 8)。
> 因此，所需操作总数为 2。
> 
> **输入:** X = 3，Y = 6
> T3】输出:否

**方法:**给定的问题可以基于以下观察来解决:

*   如果 **X** 的值至少为 **Y** ，那么 **X** 总是可以通过第二次操作转换为 **Y** ，即通过 **1** 减少 **X** 。
*   [如果 **X** 为偶数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，那么可以转换为 **(3 * (X / 2))** ，大于 **X** 的所有偶数都大于 **0** 。
*   [如果 **X** 的值为奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，则 **X** 可以转换为**(X–1)**，再转换为**(3 *(X–1)/2)**，大于 **X** 。
*   因此，从上面的观察来看， **X > 3** 始终有可能将 **X** 转换为 **Y** 。
*   需要考虑以下基本情况:
    *   **X = 1:** 只有当 **Y = 1** 时，转换才有可能。
    *   **X = 2 或 X = 3:** 只有在 **Y ≤ 3** 时才有可能转换。
    *   在所有其他情况下，转换是不可能的。

按照以下步骤解决问题:

*   如果数值 **X** 大于 **4** ，则打印**“是”**。
*   如果数值 **X** 为 **1** ， **Y** 为 **1** ，则打印**“是”**。
*   如果数值 **X** 为 **2** 或**3****Y**小于 **4** ，则打印**“是”**。
*   否则，其他所有情况打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if X can be
// made equal to Y by converting
// X to (3*X/2) or (X - 1)
void check(int X, int Y)
{
    // Conditions for possible conversion
    if (X > 3) {
        cout << "Yes";
    }

    else if (X == 1 and Y == 1) {
        cout << "Yes";
    }

    else if (X == 2 and Y <= 3) {
        cout << "Yes";
    }

    else if (X == 3 and Y <= 3) {
        cout << "Yes";
    }

    // Otherwise, conversion
    // is not possible
    else {
        cout << "No";
    }
}

// Driver Code
int main()
{
    int X = 6, Y = 8;
    check(X, Y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to check if X can be
// made equal to Y by converting
// X to (3*X/2) or (X - 1)
static void check(int X, int Y)
{

    // Conditions for possible conversion
    if (X > 3)
    {
        System.out.print("Yes");
    }

    else if (X == 1 && Y == 1)
    {
        System.out.print("Yes");
    }

    else if (X == 2 && Y <= 3)
    {
        System.out.print("Yes");
    }

    else if (X == 3 && Y <= 3)
    {
        System.out.print("Yes");
    }

    // Otherwise, conversion
    // is not possible
    else
    {
        System.out.print("No");
    }
}

// Driver Code
public static void main (String[] args)
{
    int X = 6, Y = 8;

    check(X, Y);
}
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if X can be
# made equal to Y by converting
# X to (3*X/2) or (X - 1)
def check(X, Y):

    # Conditions for possible conversion
    if (X > 3):
        print("Yes")

    elif (X == 1 and Y == 1):
        print("Yes")

    elif (X == 2 and Y <= 3):
        print("Yes")

    elif (X == 3 and Y <= 3):
        print("Yes")

    # Otherwise, conversion
    # is not possible
    else:
        print("No")

# Driver Code
if __name__ == '__main__':

    X = 6
    Y = 8

    check(X, Y)

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if X can be
// made equal to Y by converting
// X to (3*X/2) or (X - 1)
static void check(int X, int Y)
{

    // Conditions for possible conversion
    if (X > 3)
    {
        Console.WriteLine("Yes");
    }

    else if (X == 1 && Y == 1)
    {
        Console.WriteLine("Yes");
    }

    else if (X == 2 && Y <= 3)
    {
        Console.WriteLine("Yes");
    }

    else if (X == 3 && Y <= 3)
    {
        Console.WriteLine("Yes");
    }

    // Otherwise, conversion
    // is not possible
    else
    {
        Console.WriteLine("No");
    }
}

// Driver Code
public static void Main(string[] args)
{
    int X = 6, Y = 8;

    check(X, Y);
}
}

// This code is contributed by avijitmondal1998
```

## java 描述语言

```
<script>

    // JavaScript program for the above approach

    // Function to check if X can be
    // made equal to Y by converting
    // X to (3*X/2) or (X - 1)
    function check(X, Y)
    {

        // Conditions for possible conversion
        if (X > 3)
        {
            document.write("Yes");
        }

        else if (X == 1 && Y == 1)
        {
            document.write("Yes");
        }

        else if (X == 2 && Y <= 3)
        {
            document.write("Yes");
        }

        else if (X == 3 && Y <= 3)
        {
            document.write("Yes");
        }

        // Otherwise, conversion
        // is not possible
        else
        {
            document.write("No");
        }
    }

    let X = 6, Y = 8;

    check(X, Y);

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)