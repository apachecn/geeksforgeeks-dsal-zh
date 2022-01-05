# 用给定的和与异或构造最小可能数组

> 原文:[https://www . geeksforgeeks . org/construct-最小可能数组与给定和异或/](https://www.geeksforgeeks.org/construct-the-smallest-possible-array-with-given-sum-and-xor/)

给定两个正整数 **S** 和 **X** ，表示数组所有元素的和[按位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)**arr[]**。任务是找到数组的元素 **arr[]** 。如果无法生成这样的数组，请打印-1。
**举例:**

> **输入:**和= 4，异或= 2
> **输出:** {3，1}
> **说明:**
> 1 和 3 之和为 4。
> 1 和 3 的按位异或是 2。
> **输入:**和= 5，异或= 8
> **输出:** -1
> **说明:**
> 不存在这样的数组。

**方法:**可以证明数组的最大长度将最多为 3。让我们考虑以下情况:

*   **情况 1:** 如果给定的 Sum 和 Bitwise XOR 相等且非零，那么，该元素将是所需数组的唯一元素。

*   **情况 2:** 对于不等和按位异或，最短数组长度可以是 2 或 3。
    如果给定的按位异或和和分别是 a 和 b，那么通过使用异或的以下两个性质，最短数组可以是{a，(b–a)/2，(b-a)/2 }:
    *   a Xor 0 = a
    *   a Xor a = 0
*   **情况 3:** 当数组长度可以为 2 时。
    如果可能的话，我们在前一种情况下采用的数组可以简化为两个元素。

这里有一个重要的公式是有用的

> **p + q = (p ^ q) + 2*(p & q)**

在上面的公式中代入和与异或的值，我们得到一个非常有用的关系。

> b = a+2 *(p & q)
> (p&q)=(B- a)/2
> 从前例来看，
> x = (b-a)/2 = (p & q)

那么，现在让我们看看 a(给定 xor)和 x ((b-a)/2)之间的一些关系。

```
p  q  a=(p^q)  x=(p&q)  a&x
0  0    0        0       0
0  1    1        0       0
1  0    1        0       0
1  1    0        1       0
```

*   **注:** p 和 q 代表数组中两个数的所有对应的 32 位。

需要注意的是，如果 **a & x** 变成**零**那么 **a + x = a ^ x** 这意味着数组将减少到 **{a+x，x}** ，因为 **a+x = a^x** 。从上面的公式，这仍然可以导致整体异或为 a，和仍然会是 b，因为 x 是(b-a)/2。

*   **情况 4:** 剩下的唯一情况就是检查数组是否存在。在这种情况下，只有两个条件需要检查:
    1.  如果按位异或大于和。
    2.  如果 sum 和 xor 具有不同的奇偶性，即一个是偶数，另一个是奇数。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find array
void findArray(int sum, int xorr)
{
    // array not possible
    if (xorr > sum
        || sum % 2 != xorr % 2) {
        cout << "No Array Possible\n";
        return;
    }

    // Array possible with exactly 1
    // or no element
    if (sum == xorr) {
        if (sum == 0)
            cout << "Array is empty"
                 << " with size 0\n";
        else
            cout << "Array size is "
                 << 1
                 << "\n Array is "
                 << sum << "\n";
        return;
    }

    int mid = (sum - xorr) / 2;

    // Checking array with two
    // elements possible or not.
    if (xorr & mid == 1) {
        cout << "Array size is "
             << 3 << "\n";

        cout << "Array is "
             << xorr << " "
             << mid << " "
             << mid << "\n";
    }
    else {

        cout << "Array size is "
             << 2 << "\n";

        cout << "Array is "
             << (xorr + mid)
             << " "
             << mid << "\n";
    }
}

// Driver Code
int main()
{
    // Given sum and value
    // of Bitwise XOR
    int sum = 4, xorr = 2;

    // Function Call
    findArray(sum, xorr);
    cout << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program implementation
// of the approach
import java.util.*;
import java.io.*;

class GFG{

// Function to find array
static void findArray(int sum, int xorr)
{

    // Array not possible
    if (xorr > sum  || sum % 2 != xorr % 2)
    {
        System.out.println("No Array Possible");
        return;
    }

    // Array possible with exactly 1
    // or no element
    if (sum == xorr)
    {
        if (sum == 0)
            System.out.println("Array is empty " +
                               "with size 0");
        else
            System.out.println("Array size is " + 1);
            System.out.println("Array is " + sum);

            return;
    }
    int mid = (sum - xorr) / 2;

    // Checking array with two
    // elements possible or not.
    if (xorr == 1 && mid == 1)
    {
        System.out.println("Array size is " + 3);
        System.out.println("Array is " + xorr +
                              " " + mid + " " + mid);
    }
    else
    {
        System.out.println("Array size is " + 2);
        System.out.println("Array is " + (xorr + mid) +
                                           " " + mid);
    }
}

// Driver code
public static void main(String[] args)
{

    // Given sum and value
    // of Bitwise XOR
    int sum = 4, xorr = 2;

    // Function call
    findArray(sum, xorr);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find array
def findArray(_sum, xorr):

    # Array not possible
    if (xorr > _sum or
        _sum % 2 != xorr % 2):
        print("No Array Possible")
        return

    # Array possible with exactly 1
    # or no element
    if (_sum == xorr):
        if (_sum == 0):
            print("Array is empty",
                  " with size 0")

        else:
            print("Array size is", 1)
            print("Array is", _sum)
        return

    mid = (_sum - xorr) // 2

    # Checking array with two
    # elements possible or not.
    if (xorr & mid == 1):
        print("Array size is", 3)
        print("Array is", xorr, mid, mid)

    else:
        print("Array size is", 2)

        print("Array is" ,(xorr + mid), mid)

# Driver Code

# Given sum and value
# of Bitwise XOR
_sum = 4
xorr = 2

# Function Call
findArray(_sum, xorr)

# This code is contributed by divyamohan123
```

## C#

```
// C# program implementation
// of the approach
using System;

class GFG{

// Function to find array
static void findArray(int sum, int xorr)
{

    // Array not possible
    if (xorr > sum || sum % 2 != xorr % 2)
    {
        Console.WriteLine("No Array Possible");
        return;
    }

    // Array possible with exactly 1
    // or no element
    if (sum == xorr)
    {
        if (sum == 0)
            Console.WriteLine("Array is empty " +
                              "with size 0");
        else
            Console.WriteLine("Array size is " + 1);
            Console.WriteLine("Array is " + sum);
            return;
    }
    int mid = (sum - xorr) / 2;

    // Checking array with two
    // elements possible or not.
    if (xorr == 1 && mid == 1)
    {
        Console.WriteLine("Array size is " + 3);
        Console.WriteLine("Array is " + xorr +
                             " " + mid + " " + mid);
    }
    else
    {
        Console.WriteLine("Array size is " + 2);
        Console.WriteLine("Array is " + (xorr + mid) +
                                          " " + mid);
    }
}

// Driver code
public static void Main()
{

    // Given sum and value
    // of Bitwise XOR
    int sum = 4, xorr = 2;

    // Function call
    findArray(sum, xorr);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript program implementation
// of the approach

// Function to find array
function findArray(sum, xorr)
{

    // Array not possible
    if (xorr > sum  || sum % 2 != xorr % 2)
    {
        System.out.println("No Array Possible");
        return;
    }

    // Array possible with exactly 1
    // or no element
    if (sum == xorr)
    {
        if (sum == 0)
            document.write("Array is empty " +
                               "with size 0");
        else
            document.write("Array size is " + 1);
            document.write(" Array is " + sum);

            return;
    }
    var mid = (sum - xorr) / 2;

    // Checking array with two
    // elements possible or not.
    if (xorr == 1 && mid == 1)
    {
        document.write("Array size is " + 3);
        document.write("Array is " + xorr +
                         " " + mid + " " + mid);
    }
    else
    {
        document.write("Array size is " + 2);
        document.write("<br>")
        document.write("Array is " + (xorr + mid) +
                                       " " + mid);
    }
}

// Driver code

// Given sum and value
// of Bitwise XOR
var sum = 4, xorr = 2;

// Function call
findArray(sum, xorr);

// This code is contributed by Khushboogoyal499

</script>
```

**Output:** 

```
Array size is 2
Array is 3 1
```

**时间复杂度:***O(1)*
T5】辅助空间: *O(1)*