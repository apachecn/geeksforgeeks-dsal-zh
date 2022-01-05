# 检查两个数字的位数是否相同

> 原文:[https://www . geesforgeks . org/check-if-two-numbers-具有相同的位数/](https://www.geeksforgeeks.org/check-if-two-numbers-have-same-number-of-digits/)

给定两个整数 **A** 和 **B** ，任务是检查两个数字的位数是否相等。
**例:**

> **输入:** A = 12，B = 1
> **输出:**否
> **输入:** A = 20，B = 99
> **输出:**是

**逼近:**当两个数都是> 0 时，继续将两个数除以 10。最后，检查两个数字是否都是 0。如果其中任何一个不是 0，那么它们的位数就不相等。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that return true if A and B
// have same number of digits
bool sameLength(int A, int B)
{
    while (A > 0 && B > 0) {
        A = A / 10;
        B = B / 10;
    }

    // Both must be 0 now if
    // they had same lengths
    if (A == 0 && B == 0)
        return true;
    return false;
}

// Driver code
int main()
{
    int A = 21, B = 1;

    if (sameLength(A, B))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function that return true if A and B
// have same number of digits
static boolean sameLength(int A, int B)
{
    while ((A > 0) && (B > 0))
    {
        A = A / 10;
        B = B / 10;
    }

    // Both must be 0 now if
    // they had same lengths
    if ((A == 0 )&& (B == 0))
        return true;
    return false;
}

// Driver code
public static void main (String[] args)
{

    int A = 21, B = 1;
    if (sameLength(A, B))
        System.out.println ("Yes");
    else
        System.out.println("No");

}
}

// This code is contributed by @tushil.
```

## 蟒蛇 3

```

# Python implementation of the approach

# Function that return true if A and B
# have same number of digits
def sameLength(A, B):
    while (A > 0 and B > 0):
        A = A / 10;
        B = B / 10;

    # Both must be 0 now if
    # they had same lengths
    if (A == 0 and B == 0):
        return True;
    return False;

# Driver code
A = 21; B = 1;

if (sameLength(A, B)):
    print("Yes");
else:
    print("No");

# This code contributed by PrinciRaj1992
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function that return true if A and B
// have same number of digits
static bool sameLength(int A, int B)
{
    while ((A > 0) && (B > 0))
    {
        A = A / 10;
        B = B / 10;
    }

    // Both must be 0 now if
    // they had same lengths
    if ((A == 0 )&& (B == 0))
        return true;
    return false;
}

// Driver code
static public void Main ()
{

    int A = 21, B = 1;
    if (sameLength(A, B))
            Console.WriteLine("Yes");
    else
        Console.WriteLine("No");

}
}

// This code is contributed by ajit..
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that return true if A and B
// have same number of digits
function sameLength(A, B)
{
    while (A > 0 && B > 0) {
        A = parseInt(A / 10);
        B = parseInt(B / 10);
    }

    // Both must be 0 now if
    // they had same lengths
    if (A == 0 && B == 0)
        return true;
    return false;
}

// Driver code
    let A = 21, B = 1;

    if (sameLength(A, B))
        document.write("Yes");
    else
        document.write("No");

</script>
```

**Output:** 

```
No
```