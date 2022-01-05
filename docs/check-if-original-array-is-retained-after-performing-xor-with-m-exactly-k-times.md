# 在与 M 恰好 K 次执行异或运算后检查原始数组是否保留

> 原文:[https://www . geesforgeks . org/check-if-original-array-is-retention-with-m-exor-k-times/](https://www.geeksforgeeks.org/check-if-original-array-is-retained-after-performing-xor-with-m-exactly-k-times/)

给定一个数组 **A** 和两个整数 **M** 和 **K** ，任务是检查并打印“ **Yes** ”，如果通过对数组元素执行精确的“ **K** ”数量的[位异或](https://www.geeksforgeeks.org/tag/xor/)运算可以保留原始数组，则带有“ **M** ”。否则打印“**否**”。
**注意:**可以对数组的任意元素进行 0 次或更多次异或运算。
**例:**

> **输入:** A[] = {1，2，3，4}，M = 5，K = 6
> **输出:**是
> **说明:**
> 如果对第 1 个元素 A[0]进行异或运算，6 次，我们得到 A[0]回来。因此，原始数组被保留。
> **输入:** A[] = {5，9，3，4，5}，M = 5，K = 3
> **输出:**否
> **说明:**
> 执行奇数次异或运算后无法保留原数组。

**方法:**这个问题可以使用[异或属性](https://www.geeksforgeeks.org/bitwise-hacks-for-competitive-programming/)T4 来解决

> 一个异或 B = C 和 C 异或 B = A

可以看出:

1.  如果对任何正数执行偶数个异或运算，则可以保留原始数。
2.  但是，0 是一个例外。如果对 0 执行奇数或偶数个异或运算，则可以保留原始数。
3.  因此**如果 K 为偶数，M 为 0** ，那么答案永远是肯定的。
4.  **如果 K 为奇数，数组**中不存在 0，则答案始终为否
5.  **如果 K 是奇数，并且数组中 0 的计数至少为 1** ，则答案为是。

**以下是上述方法的实施:**

## C++

```
// C++ implementation for the
// above mentioned problem

#include <bits/stdc++.h>
using namespace std;

// Function to check if original Array
// can be retained by performing XOR
// with M exactly K times
string check(int Arr[], int n,
             int M, int K)
{
    int flag = 0;

    // Check if O is present or not
    for (int i = 0; i < n; i++) {
        if (Arr[i] == 0)
            flag = 1;
    }

    // If K is odd and 0 is not present
    // then the answer will always be No.
    if (K % 2 != 0
        && flag == 0)
        return "No";

    // Else it will be Yes
    else
        return "Yes";
}

// Driver Code
int main()
{

    int Arr[] = { 1, 1, 2, 4, 7, 8 };
    int M = 5;
    int K = 6;
    int n = sizeof(Arr) / sizeof(Arr[0]);

    cout << check(Arr, n, M, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

class GFG{

// Function to check if original Array
// can be retained by performing XOR
// with M exactly K times
static String check(int []Arr, int n,
            int M, int K)
{
    int flag = 0;

    // Check if O is present or not
    for (int i = 0; i < n; i++) {
        if (Arr[i] == 0)
            flag = 1;
    }

    // If K is odd and 0 is not present
    // then the answer will always be No.
    if (K % 2 != 0
        && flag == 0)
        return "No";

    // Else it will be Yes
    else
        return "Yes";
}

// Driver Code
public static void main(String args[])
{

    int []Arr = { 1, 1, 2, 4, 7, 8 };
    int M = 5;
    int K = 6;
    int n = Arr.length;

    System.out.println(check(Arr, n, M, K));
}
}

// This code is contributed by Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 implementation for the
# above mentioned problem

# Function to check if original Array
# can be retained by performing XOR
# with M exactly K times
def check(Arr,  n, M,  K):
    flag = 0

    # Check if O is present or not
    for i in range(n):
        if (Arr[i] == 0):
            flag = 1

    # If K is odd and 0 is not present
    # then the answer will always be No.
    if (K % 2 != 0 and flag == 0):
        return "No"

    # Else it will be Yes
    else:
        return "Yes";

# Driver Code
if __name__=='__main__':

    Arr = [ 1, 1, 2, 4, 7, 8 ]
    M = 5;
    K = 6;
    n = len(Arr);

    print(check(Arr, n, M, K))

# This article contributed by Princi Singh
```

## C#

```
// C# implementation for the
// above mentioned problem
using System;

class GFG
{

// Function to check if original Array
// can be retained by performing XOR
// with M exactly K times
static String check(int []Arr, int n,int M, int K)
{
    int flag = 0;

    // Check if O is present or not
    for (int i = 0; i < n; i++) {
        if (Arr[i] == 0)
            flag = 1;
    }

    // If K is odd and 0 is not present
    // then the answer will always be No.
    if (K % 2 != 0
        && flag == 0)
        return "No";

    // Else it will be Yes
    else
        return "Yes";
}

// Driver code
public static void Main(String[] args)
{

    int []Arr = { 1, 1, 2, 4, 7, 8 };
    int M = 5;
    int K = 6;
    int n = Arr.Length;

    Console.Write(check(Arr, n, M, K));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
// Javascript implementation for the
// above mentioned problem

// Function to check if original Array
// can be retained by performing XOR
// with M exactly K times
function check(Arr, n, M, K)
{
    let flag = 0;

    // Check if O is present or not
    for (let i = 0; i < n; i++) {
        if (Arr[i] == 0)
            flag = 1;
    }

    // If K is odd and 0 is not present
    // then the answer will always be No.
    if (K % 2 != 0
        && flag == 0)
        return "No";

    // Else it will be Yes
    else
        return "Yes";
}

// Driver Code

    let Arr = [ 1, 1, 2, 4, 7, 8 ];
    let M = 5;
    let K = 6;
    let n = Arr.length;

    document.write(check(Arr, n, M, K));

</script>
```

**Output:** 

```
Yes
```

时间复杂度:0(N)

辅助空间:0(1)