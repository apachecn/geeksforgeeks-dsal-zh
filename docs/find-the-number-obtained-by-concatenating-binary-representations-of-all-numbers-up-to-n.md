# 找出所有数字的二进制表示串联起来得到的数字，直到 N

> 原文:[https://www . geeksforgeeks . org/find-通过串联所有数字的二进制表示获得的数字-高达 n/](https://www.geeksforgeeks.org/find-the-number-obtained-by-concatenating-binary-representations-of-all-numbers-up-to-n/)

给定一个整数 **N** ，任务是找到[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/)的十进制值，该字符串是由从 **1 到 N** 的所有数字的二进制表示顺序串联而成的。

**示例:**

> **输入:** N = 12
> **输出:** 118505380540
> **说明:**串接结果为“11011110011011100001001101010101010111111100”。等效十进制值为 118505380540。
> 
> **输入:** N = 3
> **输出:** 27
> **说明:**在二进制中，1、2、3 对应“1”、“10”、“11”。它们的连接导致“11011”，对应于十进制值 27。

**方法:**思路是迭代范围**【1，N】**。对于每一个 **i <sup>第</sup>** 个数字，使用[逐位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)属性连接数字 **i** 的二进制表示。按照以下步骤解决问题:

1.  初始化两个变量， **l** ，用 **0** 初始化 **ans** ，其中 **l** 存储任意 **i <sup>th</sup>** 号的最终二进制字符串中该位的当前位置， **ans** 将存储最终答案。
2.  从 **i = 1 迭代到 N + 1** 。
3.  如果**(I&(I–1))**等于 **0** ，那么只需将 **l** 的值增加 **1** ，其中 **&** 为[位与运算符](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)。
4.  之后，左移位**用 **l** 代替**，然后[用 **i** 对结果进行逐位“或”。](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)
5.  和遍历后，打印**和**作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the decimal value by
// concatenating the numbers from 1 to N
int concatenatedBinary(int n)
{

    // Stores count of
    // bits in a number
    int l = 0;

    // Stores decimal value by
    // concatenating 1 to N
    int ans = 0;

    // Iterate over the range [1, n]
    for (int i = 1; i < n + 1; i++){

        // If i is a power of 2
        if ((i & (i - 1)) == 0)
              l += 1;

        // Update ans
        ans = ((ans << l) | i);
    }

    // Return ans
    return ans;
}

// Driver Code
int main()
{
    int n = 3;

    // Function Call
    cout << (concatenatedBinary(n));

  return 0;
}

// This code is contributed by mohiy kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{

    // Function to find the decimal value by
    // concatenating the numbers from 1 to N
    static int concatenatedBinary(int n)
    {

        // Stores count of
        // bits in a number
        int l = 0;

        // Stores decimal value by
        // concatenating 1 to N
        int ans = 0;

        // Iterate over the range [1, n]
        for (int i = 1; i < n + 1; i++){

            // If i is a power of 2
            if ((i & (i - 1)) == 0)
                  l += 1;

            // Update ans
            ans = ((ans << l) | i);
        }

        // Return ans
        return ans;
    }

    // Driver Code
    public static void main (String[] args)
    {
        int n = 3;

        // Function Call
        System.out.println(concatenatedBinary(n));
    }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the decimal value by
# concatenating the numbers from 1 to N
def concatenatedBinary(n):

    # Stores count of
    # bits in a number
    l = 0

    # Stores decimal value by
    # concatenating 1 to N
    ans = 0

    # Iterate over the range [1, n]
    for i in range(1, n + 1):

        # If i is a power of 2
        if i & (i - 1) == 0:

            # Update l
            l += 1

        # Update ans
        ans = ((ans << l) | i)

    # Return ans
    return(ans)

# Driver Code
if __name__ == '__main__':
    n = 3

    # Function Call
    print(concatenatedBinary(n))
```

## C#

```
// C# program to implement
// the above approach 
using System;
class GFG
{

    // Function to find the decimal value by
    // concatenating the numbers from 1 to N
    static int concatenatedBinary(int n)
    {

        // Stores count of
        // bits in a number
        int l = 0;

        // Stores decimal value by
        // concatenating 1 to N
        int ans = 0;

        // Iterate over the range [1, n]
        for (int i = 1; i < n + 1; i++)
        {

            // If i is a power of 2
            if ((i & (i - 1)) == 0)
                  l += 1;

            // Update ans
            ans = ((ans << l) | i);
        }

        // Return ans
        return ans;
    }

    // Driver Code
    public static void Main ()
    {
        int n = 3;

        // Function Call
        Console.WriteLine(concatenatedBinary(n));
    }
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>
//Javascript program to implement
// the above approach

// Function to find the decimal value by
// concatenating the numbers from 1 to N
function concatenatedBinary(n)
{

    // Stores count of
    // bits in a number
    var l = 0;

    // Stores decimal value by
    // concatenating 1 to N
    var ans = 0;

    // Iterate over the range [1, n]
    for (var i = 1; i < n + 1; i++){

        // If i is a power of 2
        if ((i & (i - 1)) == 0)
              l += 1;

        // Update ans
        ans = parseInt((ans << l) | i);
    }

    // Return ans
    return ans;
}

var n = 3;
// Function Call
document.write(concatenatedBinary(n));

//This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
27
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)