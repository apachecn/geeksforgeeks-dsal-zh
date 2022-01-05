# 以 MEX 为 A，数组元素异或为 B 的数组最小尺寸

> 原文:[https://www . geeksforgeeks . org/最小大小的数组以 mex 作为数组元素的 a 和 xor 作为 b/](https://www.geeksforgeeks.org/minimum-size-of-the-array-with-mex-as-a-and-xor-of-the-array-elements-as-b/)

给定两个整数 **A** 和 **B** ，任务是找到数组的最小可能[大小，其数组](https://www.geeksforgeeks.org/how-to-find-size-of-array-in-cc-without-using-sizeof-operator/) **的 [**MEX** 为**A**](https://www.geeksforgeeks.org/construct-mex-array-from-the-given-array/)[和**按位** **异或**](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/) **所有数组元素的**为 **B** 。**

**示例:**

> **输入:** A = 1，B = 1
> **输出:** 3
> **说明:**能满足给定条件的数组是{0，3，2}，它的可能大小是最小的，即 3。
> 
> **输入:** A = 1，B = 999
> T3】输出: 2

**方法:**给定的问题可以通过以下观察来解决:

*   因为阵列的 MEX 应该是 **A** ，因为必须包括范围**【0，A–1】**内的所有元素。
*   为了使所有数组元素的[异或为 **B** ，必须在数组中加入几个整数，可以分为 3 种情况。假设变量 **currXOR** 存储了范围**【0，A–1】**内的 XOR 值，可以使用本文](https://www.geeksforgeeks.org/find-xor-of-all-elements-in-an-array/)中讨论的方法进行计算。
    *   第一种情况 **currXor = B** 。在这种情况下，不需要添加整数。
    *   情况 2，其中 **currXor^B = A** 。在这种情况下，由于 **A** 不能添加到数组中， **2** 整数必须相加，这样它们的**异或**就是 **A** 。
    *   在所有其他情况下， **1** 整数必须相加，以使给定数组的**异或**为 **B** 。

因此，上述问题可以通过[求从 0 到 A-1 的所有数字的异或](https://www.geeksforgeeks.org/calculate-xor-1-n/)并检查上述情况来解决。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum size
// of array with given MEX and XOR
int minimumSizeArr(int A, int B)
{
    int currXor = 0;

    // Find the XOR of values from
    // 0 to A-1
    int reminder = (A - 1) % 4;

    // If A is a multiple of 4
    if (reminder == 0)
        currXor = A - 1;

    // If A % 4 gives remainder 1
    else if (reminder == 1)
        currXor = 1;

    // If A % 4 gives remainder 2
    else if (reminder == 2)
        currXor = A;

    // Initializing array size by A
    int minSize = A;

    // If XOR of all values of array
    // is equal to B
    if (currXor == B)
        return minSize;

    // If the required integer to be
    // added is equal to A
    else if (currXor ^ B == A)
        return minSize + 2;

    // Else any integer can be added
    else
        return minSize + 1;
}

// Driver Code
int main()
{
    int A = 1;
    int B = 999;
    cout << minimumSizeArr(A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG {

    // Function to find the minimum size
    // of array with given MEX and XOR
    static int minimumSizeArr(int A, int B)
    {
        int currXor = 0;

        // Find the XOR of values from
        // 0 to A-1
        int reminder = (A - 1) % 4;

        // If A is a multiple of 4
        if (reminder == 0)
            currXor = A - 1;

        // If A % 4 gives remainder 1
        else if (reminder == 1)
            currXor = 1;

        // If A % 4 gives remainder 2
        else if (reminder == 2)
            currXor = A;

        // Initializing array size by A
        int minSize = A;

        // If XOR of all values of array
        // is equal to B
        if (currXor == B)
            return minSize;

        // If the required integer to be
        // added is equal to A
        else if ((currXor ^ B) == A)
            return minSize + 2;

        // Else any integer can be added
        else
            return minSize + 1;
    }

    // Driver Code
    public static void main (String[] args) {

        int A = 1;
        int B = 999;
        System.out.println(minimumSizeArr(A, B));       
    }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# python program for the above approach

# Function to find the minimum size
# of array with given MEX and XOR
def minimumSizeArr(A, B):

    currXor = 0

    # Find the XOR of values from
    # 0 to A-1
    reminder = (A - 1) % 4

    # If A is a multiple of 4
    if (reminder == 0):
        currXor = A - 1

    # If A % 4 gives remainder 1
    elif (reminder == 1):
        currXor = 1

    # If A % 4 gives remainder 2
    elif (reminder == 2):
        currXor = A

    # Initializing array size by A
    minSize = A

    # If XOR of all values of array
    # is equal to B
    if (currXor == B):
        return minSize

    # If the required integer to be
    # added is equal to A
    elif (currXor ^ B == A):
        return minSize + 2

    # Else any integer can be added
    else:
        return minSize + 1

# Driver Code
if __name__ == "__main__":

    A = 1
    B = 999
    print(minimumSizeArr(A, B))

# This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
public class GFG {

    // Function to find the minimum size
    // of array with given MEX and XOR
    static int minimumSizeArr(int A, int B)
    {
        int currXor = 0;

        // Find the XOR of values from
        // 0 to A-1
        int reminder = (A - 1) % 4;

        // If A is a multiple of 4
        if (reminder == 0)
            currXor = A - 1;

        // If A % 4 gives remainder 1
        else if (reminder == 1)
            currXor = 1;

        // If A % 4 gives remainder 2
        else if (reminder == 2)
            currXor = A;

        // Initializing array size by A
        int minSize = A;

        // If XOR of all values of array
        // is equal to B
        if (currXor == B)
            return minSize;

        // If the required integer to be
        // added is equal to A
        else if ((currXor ^ B) == A)
            return minSize + 2;

        // Else any integer can be added
        else
            return minSize + 1;
    }

    // Driver Code
    public static void Main () {

        int A = 1;
        int B = 999;
        Console.WriteLine(minimumSizeArr(A, B));       
    }
}

// This code is contributed by ihritik
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the minimum size
// of array with given MEX and XOR
function minimumSizeArr(A, B)
{
  let currXor = 0;

  // Find the XOR of values from
  // 0 to A-1
  let reminder = (A - 1) % 4;

  // If A is a multiple of 4
  if (reminder == 0) currXor = A - 1;

  // If A % 4 gives remainder 1
  else if (reminder == 1) currXor = 1;

  // If A % 4 gives remainder 2
  else if (reminder == 2) currXor = A;

  // Initializing array size by A
  let minSize = A;

  // If XOR of all values of array
  // is equal to B
  if (currXor == B) return minSize;
  // If the required integer to be
  // added is equal to A
  else if (currXor ^ (B == A)) return minSize + 2;
  // Else any integer can be added
  else return minSize + 1;
}

// Driver Code

let A = 1;
let B = 999;
document.write(minimumSizeArr(A, B));

// This code is contributed by saurabh_jaiswal.
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)