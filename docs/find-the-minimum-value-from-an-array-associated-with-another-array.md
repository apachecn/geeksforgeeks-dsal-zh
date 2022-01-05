# 从与另一个数组关联的数组中找到最小值

> 原文:[https://www . geeksforgeeks . org/从与另一个数组关联的数组中查找最小值/](https://www.geeksforgeeks.org/find-the-minimum-value-from-an-array-associated-with-another-array/)

给定相等长度的整数数组 **A[]** 和字符数组 **B[]** ，其中数组的每个字符都来自集合 **{'a '，' B '，' c'}** 。两个数组的元素相互关联，即 **B[i]** 的值链接到 **A[i]** 的 **i** 的所有有效值。任务是找到值 **min(a + b，c)** 。

**示例:**

> **输入:** A[] = {3，6，4，5，6}，B[] = {'a '，' c '，' B '，' B '，' A ' }
> T3】输出: 6
> 
> **输入:** A[] = {4，2，6，2，3}，B[] = {'b '，' A '，' c '，' A '，' B ' }
> T3】输出: 5

**接近:**为了使所需值最小化， **a** 、 **b** 和 **c** 的值必须最小化。所以，遍历数组，找出整数数组中与这些字符相关的 **a** 、 **b** 、 **c** 的最小值，最后返回 **min(a + b，c)** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to get the minimum required value
int getMinimum(int A[], char B[], int n)
{

    // To store the minimum values
    // of 'a', 'b' and 'c'
    int minA = INT_MAX;
    int minB = INT_MAX;
    int minC = INT_MAX;

    // For every value of A[]
    for (int i = 0; i < n; i++) {
        switch (B[i]) {

        // Update the minimum values of 'a',
        // 'b' and 'c'
        case 'a':
            minA = min(A[i], minA);
            break;
        case 'b':
            minB = min(A[i], minB);
            break;
        case 'c':
            minC = min(A[i], minC);
            break;
        }
    }

    // Return the minimum required value
    return min(minA + minB, minC);
}

// Driver code
int main()
{
    int A[] = { 4, 2, 6, 2, 3 };
    char B[] = { 'b', 'a', 'c', 'a', 'b' };

    int n = sizeof(A) / sizeof(A[0]);

    cout << getMinimum(A, B, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

// Function to get the minimum required value
static int getMinimum(int A[], char B[], int n)
{

    // To store the minimum values
    // of 'a', 'b' and 'c'
    int minA = Integer.MAX_VALUE;
    int minB = Integer.MAX_VALUE;
    int minC = Integer.MAX_VALUE;

    // For every value of A[]
    for (int i = 0; i < n; i++)
    {
        switch (B[i])
        {

            // Update the minimum values of 'a',
            // 'b' and 'c'
            case 'a':
                minA = Math.min(A[i], minA);
                break;

            case 'b':
                minB = Math.min(A[i], minB);
                break;

            case 'c':
                minC = Math.min(A[i], minC);
                break;
        }
    }

    // Return the minimum required value
    return Math.min(minA + minB, minC);
}

// Driver code
public static void main(String[] args)
{
    int A[] = { 4, 2, 6, 2, 3 };
    char B[] = { 'b', 'a', 'c', 'a', 'b' };

    int n = A.length;

    System.out.println(getMinimum(A, B, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to get the minimum required value
def getMinimum(A, B, n):

    # To store the minimum values
    # of 'a', 'b' and 'c'
    minA = float('inf');
    minB = float('inf');
    minC = float('inf');

    # For every value of A[]
    for i in range(n):
        if B[i]=='a':
            minA = min(A[i], minA)
        if B[i]=='b':
            minB = min(A[i], minB)
        if B[i]=='c':
            minB = min(A[i], minC)

    # Return the minimum required value
    return min(minA + minB, minC)

# Driver code
if __name__ == '__main__':
    A = [ 4, 2, 6, 2, 3 ]
    B = [ 'b', 'a', 'c', 'a', 'b' ]
    n = len(A);

    print(getMinimum(A, B, n))

# This code is contributed by Ashutosh450
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to get the minimum required value
    static int getMinimum(int []A, char []B, int n)
    {

        // To store the minimum values
        // of 'a', 'b' and 'c'
        int minA = int.MaxValue;
        int minB = int.MaxValue;
        int minC = int.MaxValue;

        // For every value of A[]
        for (int i = 0; i < n; i++)
        {
            switch (B[i])
            {

                // Update the minimum values of 'a',
                // 'b' and 'c'
                case 'a':
                    minA = Math.Min(A[i], minA);
                    break;

                case 'b':
                    minB = Math.Min(A[i], minB);
                    break;

                case 'c':
                    minC = Math.Min(A[i], minC);
                    break;
            }
        }

        // Return the minimum required value
        return Math.Min(minA + minB, minC);
    }

    // Driver code
    public static void Main()
    {
        int []A = { 4, 2, 6, 2, 3 };
        char []B = { 'b', 'a', 'c', 'a', 'b' };

        int n = A.Length;

        Console.WriteLine(getMinimum(A, B, n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to get the minimum required value
function getMinimum(A, B, n)
{

    // To store the minimum values
    // of 'a', 'b' and 'c'
    var minA = 1000000000;
    var minB = 1000000000;
    var minC = 1000000000;

    // For every value of A[]
    for (var i = 0; i < n; i++) {
        switch (B[i]) {

        // Update the minimum values of 'a',
        // 'b' and 'c'
        case 'a':
            minA = Math.min(A[i], minA);
            break;
        case 'b':
            minB = Math.min(A[i], minB);
            break;
        case 'c':
            minC = Math.min(A[i], minC);
            break;
        }
    }

    // Return the minimum required value
    return Math.min(minA + minB, minC);
}

// Driver code
var A = [4, 2, 6, 2, 3 ];
var B = ['b', 'a', 'c', 'a', 'b'];
var n = A.length;
document.write( getMinimum(A, B, n));

</script>
```

**Output:** 

```
5
```