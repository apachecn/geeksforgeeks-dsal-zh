# 检查是否可以将 A 转换成 B

> 原文:[https://www . geesforgeks . org/check-是否有可能将 a 转换为 b/](https://www.geeksforgeeks.org/check-whether-it-is-possible-to-convert-a-into-b/)

给定两个整数 **A** 和 **B** 。任务是检查是否可以通过多次执行以下操作将 **A** 转换为 **B** 。

1.  将当前号码 **x** 转换为 **2 * x** 。
2.  将当前号码 **x** 转换为 **(10 * x) + 1** 。

**示例:**

> **输入:** A = 2，B = 82
> T3】输出:是
> 2->4->41->82
> T7】输入: A = 2，B = 5
> T10】输出:否

**方法:**我们反过来解决这个问题——试着从 **B** 那里得到 **A** 这个号码。
注意，如果 **B** 以 **1** 结束，最后一个操作是将数字 **1** 追加到当前数字的右边。因此，让我们删除 **B** 的最后一个数字，并移到新的数字。
如果最后一位是**偶数**，那么最后一个操作是将当前数字乘以 **2** 。正因为如此，让我们把 **B** 除以 2，然后移到新的数字。
在其他情况下(如果 B 以除 1 以外的**奇数结尾)，答案是**否**。
我们需要在每次得到一个新的号码后重复描述的算法。如果在某个时刻，我们得到一个等于 **A** 的数字，那么答案是**是**，如果新的数字小于 **A** ，那么答案是**否**。
以下是上述方法的实施:** 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if A can be
// converted to B with the given operations
bool canConvert(int a, int b)
{
    while (b > a) {

        // If the current number ends with 1
        if (b % 10 == 1) {
            b /= 10;
            continue;
        }

        // If the current number is divisible by 2
        if (b % 2 == 0) {
            b /= 2;
            continue;
        }

        // If above two conditions fail
        return false;
    }

    // If it is possible to convert A to B
    if (b == a)
        return true;
    return false;
}

// Driver code
int main()
{
    int A = 2, B = 82;

    if (canConvert(A, B))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function that returns true if A can be
    // converted to B with the given operations
    static boolean canConvert(int a, int b)
    {
        while (b > a)
        {

            // If the current number ends with 1
            if (b % 10 == 1)
            {
                b /= 10;
                continue;
            }

            // If the current number is divisible by 2
            if (b % 2 == 0)
            {
                b /= 2;
                continue;
            }

            // If above two conditions fail
            return false;
        }

        // If it is possible to convert A to B
        if (b == a)
            return true;
        return false;
    }

    // Driver code
    public static void main(String[] args)
    {

        int A = 2, B = 82;

        if (canConvert(A, B))
            System.out.println("Yes");
        else
            System.out.println("No");

    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if A can be
# converted to B with the given operations
def canConvert(a, b) :

    while (b > a) :

        # If the current number ends with 1
        if (b % 10 == 1) :
            b //= 10;
            continue;

        # If the current number is divisible by 2
        if (b % 2 == 0) :
            b /= 2;
            continue;

        # If the above two conditions fail
        return false;

    # If it is possible to convert A to B
    if (b == a) :
        return True;

    return False;

# Driver code
if __name__ == "__main__" :

    A = 2; B = 82;

    if (canConvert(A, B)) :
        print("Yes");
    else :
        print("No");

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

    // Function that returns true if A can be
    // converted to B with the given operations
    static bool canConvert(int a, int b)
    {
        while (b > a)
        {

            // If the current number ends with 1
            if (b % 10 == 1)
            {
                b /= 10;
                continue;
            }

            // If the current number is divisible by 2
            if (b % 2 == 0)
            {
                b /= 2;
                continue;
            }

            // If above two conditions fail
            return false;
        }

        // If it is possible to convert A to B
        if (b == a)
            return true;
        return false;
    }

    // Driver code
    public static void Main()
    {

        int A = 2, B = 82;

        if (canConvert(A, B))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");

    }
}

// This code is contributed by anuj_67..
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function that returns true if A can be
// converted to B with the given operations
function canConvert(a, b)
{
    while (b > a) {

        // If the current number ends with 1
        if (b % 10 == 1) {
            b = parseInt(b / 10);
            continue;
        }

        // If the current number is divisible by 2
        if (b % 2 == 0) {
            b = parseInt(b / 2);
            continue;
        }

        // If above two conditions fail
        return false;
    }

    // If it is possible to convert A to B
    if (b == a)
        return true;
    return false;
}

// Driver code
    let A = 2, B = 82;

    if (canConvert(A, B))
        document.write("Yes");
    else
        document.write("No");

</script>
```

**Output:** 

```
Yes
```