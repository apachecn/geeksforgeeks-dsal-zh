# 检查 N 个数的按位“与”是偶数还是奇数

> 原文:[https://www . geeksforgeeks . org/check-n-numbers 的位与是偶数还是奇数/](https://www.geeksforgeeks.org/check-whether-bitwise-and-of-n-numbers-is-even-or-odd/)

给定一个包含 **N** 个数字的数组 **arr[]** 。任务是检查给定的 **N** 数的位与是偶数还是奇数。
**示例** :

> **输入:** arr[] = { 2，12，20，36，38 }
> **输出:**偶数
> **输入:** arr[] = { 3，9，17，13，15 }
> **输出:**奇数

一个**简单的解决方法**是首先找到给定 N 个数的 AND，然后检查这个 AND 是偶数还是奇数。
一个**更好的解决方案**是基于比特操作和数学事实。

*   任意两个偶数的按位“与”是偶数。
*   任意两个奇数的按位“与”是奇数。
*   偶数和奇数的按位“与”是偶数。

基于以上事实，可以推断，如果数组中至少存在一个偶数，则整个数组的按位“与”将是偶数，否则将是奇数。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if the bitwise AND
// of the array elements is even or odd
void checkEvenOdd(int arr[], int n)
{
    for (int i = 0; i < n; i++) {

        // If at least an even element is present
        // then the bitwise AND of the
        // array elements will be even
        if (arr[i] % 2 == 0) {

            cout << "Even";
            return;
        }
    }

    cout << "Odd";
}

// Driver code
int main()
{
    int arr[] = { 2, 12, 20, 36, 38 };
    int n = sizeof(arr) / sizeof(arr[0]);

    checkEvenOdd(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function to check if the bitwise AND
// of the array elements is even or odd
static void checkEvenOdd(int []arr, int n)
{
    for (int i = 0; i < n; i++)
    {

        // If at least an even element is present
        // then the bitwise AND of the
        // array elements will be even
        if (arr[i] % 2 == 0)
        {
            System.out.print("Even");
            return;
        }
    }
    System.out.println("Odd");
}

// Driver code
public static void main (String[] args)
{
    int []arr = { 2, 12, 20, 36, 38 };
    int n = arr.length;

    checkEvenOdd(arr, n);
}
}

// This code is contributed by @tushil
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to check if the bitwise AND
# of the array elements is even or odd
def checkEvenOdd(arr, n) :

    for i in range(n) :

        # If at least an even element is present
        # then the bitwise AND of the
        # array elements will be even
        if (arr[i] % 2 == 0) :

            print("Even", end = "");
            return;

    print("Odd", end = "");

# Driver code
if __name__ == "__main__" :

    arr = [ 2, 12, 20, 36, 38 ];
    n = len(arr);

    checkEvenOdd(arr, n);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to check if the bitwise AND
// of the array elements is even or odd
static void checkEvenOdd(int []arr, int n)
{
    for (int i = 0; i < n; i++)
    {

        // If at least an even element is present
        // then the bitwise AND of the
        // array elements will be even
        if (arr[i] % 2 == 0)
        {
            Console.Write ("Even");
            return;
        }
    }
    Console.Write ("Odd");
}

// Driver code
static public void Main ()
{
    int []arr = { 2, 12, 20, 36, 38 };
    int n = arr.Length;

    checkEvenOdd(arr, n);
}
}

// This code is contributed by ajit..
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to check if the bitwise AND
    // of the array elements is even or odd
    function checkEvenOdd(arr, n)
    {
        for (let i = 0; i < n; i++) 
        {

            // If at least an even element is present
            // then the bitwise AND of the
            // array elements will be even
            if (arr[i] % 2 == 0) 
            {
                document.write ("Even");
                return;
            }
        }
        document.write ("Odd");
    }

    let arr = [ 2, 12, 20, 36, 38 ];
    let n = arr.length;

    checkEvenOdd(arr, n);

</script>
```

**Output:** 

```
Even
```

**时间复杂度:** O(N)