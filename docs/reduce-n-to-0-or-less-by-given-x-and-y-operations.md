# 通过给定的 X 和 Y 操作将 N 减少到 0 或更少

> 原文:[https://www . geesforgeks . org/reduce-n-to-0-or-less-by-given-x-and-y-operations/](https://www.geeksforgeeks.org/reduce-n-to-0-or-less-by-given-x-and-y-operations/)

给定三个整数 **N** 、 **X、**和 **Y、**，任务是检查是否可以通过以下操作将 **N** 减少到 0 或更少:

*   更新 **N** 到 **⌊N/2⌋ + 10，**最多 **X** 次
*   更新 **N** 到**N–10，**最多 **Y** 次。

**示例:**

> **输入:** N = 100，X = 3，Y = 4
> **输出:** Yes
> **解释:**
> 更新 N = 100 到⌊100/2⌋ + 10 = 60。
> 更新 N = 60 至 60 10 = 50。
> 将 N = 50 更新为⌊50/2⌋ + 10 = 35。
> 将 N = 35 更新为⌊35/2⌋ + 10 = 27。
> 更新 N = 27 至 27 10 = 17。
> 更新 N = 17 到 1710 = 7。
> 更新 N = 7 至 7 10 = 3。
> 
> **输入:** N = 50，X = 1，Y = 2
> T3】输出:否

**方法:**这个问题可以根据以下观察来解决:

*   **情况 1:** 如果 **⌊N/2⌋ + 10 > = N** ，那么只执行第二次操作，因为第一次操作会增加数值 **N** 。
*   **情况 2:** 如果先执行第一个操作，然后执行第二个操作，则结果为:

> 操作 1 = n/2 = 10
> 操作 2:(897n/2⌒10)—10 = n/2℃

*   **N** 的值减少到 **(⌊N/2⌋)** 。
*   **情况 3:** 如果执行第二次操作后接着执行第一次操作，则结果为:

> 操作 2:n = n-10
> 操作 1:操作 1:n-10/2⌒10 =(⌒n/2-5+10)=(⌒n/2⌒5)

*   **N** 的值降为 **(⌊N/2⌋ + 5)** 。

从以上两个观察，如果 **N > N/2 +10** ，那么可以得出结论，要将 **N** 的值减小到 **0** 或更小，第一次操作必须在第二次操作之前进行，以减小 **N** 的值。
按照以下步骤解决问题:

1.  如果 N > N/2 + 10 和 X > 0，则将 **N** 的值更新为 **⌊N/2⌋ + 10** 。
2.  最多 Y 次将 **N** 的值更新为**N–10**。
3.  检查 **N** 的更新值是否小于等于 0。
4.  如果 N ≤ 0，则打印**“是”**。否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if N can be
// reduced to <= 0 or not
bool NegEqu(int N, int X, int Y)
{

    // Update N to N/2 + 10 at most X times
    while (X-- and N > N/2 + 10) {
        N = N / 2 + 10;
    }

    // Update N to N - 10 Y times
    while (Y--) {
        N = N - 10;
    }

    if (N <= 0)
        return true;

    return false;
}

// Driver Code
int main()
{
    int N = 100;
    int X = 3;
    int Y = 4;

    if (NegEqu(N, X, Y)) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Function to check if N can be
// reduced to <= 0 or not
static boolean NegEqu(int N, int X, int Y)
{

    // Update N to N/2 + 10 at most X times
    while (X > 0 && (N > N / 2 + 10))
    {
        N = N / 2 + 10;
        X -= 1;
    }

    // Update N to N - 10 Y times
    while (Y > 0)
    {
        N = N - 10;
        Y -= 1;
    }

    if (N <= 0)
        return true;

    return false;
}

// Driver Code
public static void main(String[] args)
{
    int N = 100;
    int X = 3;
    int Y = 4;

    if (NegEqu(N, X, Y))
    {
        System.out.println("Yes");
    }
    else
    {
        System.out.println("No");
    }
}
}

// This code is contributed by jana_sayantan
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check if N can be
# reduced to <= 0 or not
def NegEqu(N, X, Y):

    # Update N to N/2 + 10 at most X times
    while (X and N > N // 2 + 10):
        N = N // 2 + 10
        X -= 1

    # Update N to N - 10 Y times
    while (Y):
        N = N - 10
        Y -= 1

    if (N <= 0):
        return True

    return False

# Driver Code
if __name__ == '__main__':

    N = 100
    X = 3
    Y = 4

    if (NegEqu(N, X, Y)):
        print("Yes")
    else:
        print("No")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to check if N can be
// reduced to <= 0 or not
public static bool NegEqu(int N, int X,
                          int Y)
{

    // Update N to N/2 + 10 at most X times
    while (X > 0 && (N > N / 2 + 10))
    {
        N = N / 2 + 10;
        X -= 1;
    }

    // Update N to N - 10 Y times
    while (Y > 0)
    {
        N = N - 10;
        Y -= 1;
    }

    if (N <= 0)
        return true;

    return false;
}

// Driver Code
public static void Main(String[] args)
{
    int N = 100;
    int X = 3;
    int Y = 4;

    if (NegEqu(N, X, Y))
    {
        Console.WriteLine("Yes");
    }
    else
    {
        Console.WriteLine("No");
    }
}
}

// This code is contributed by jana_sayantan
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Function to check if N can be
// reduced to <= 0 or not
function NegEqu(N, X, Y)
{

    // Update N to N/2 + 10 at most X times
    while (X > 0 && (N > N / 2 + 10))
    {
        N = N / 2 + 10;
        X -= 1;
    }

    // Update N to N - 10 Y times
    while (Y > 0)
    {
        N = N - 10;
        Y -= 1;
    }

    if (N <= 0)
        return true;

    return false;
}

// Driver code

    let N = 100;
    let X = 3;
    let Y = 4;

    if (NegEqu(N, X, Y))
    {
        document.write("Yes");
    }
    else
    {
        document.write("No");
    }

  // This code is contributed by code_hunt.
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(X + Y)*
***辅助空间** :O(1)*