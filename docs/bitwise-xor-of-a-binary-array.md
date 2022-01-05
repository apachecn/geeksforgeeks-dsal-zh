# 二进制数组的逐位异或

> 原文:[https://www . geeksforgeeks . org/二进制数组按位异或/](https://www.geeksforgeeks.org/bitwise-xor-of-a-binary-array/)

给定一个二进制数组 **arr[]** ，任务是计算这个数组中所有元素的按位异或并打印出来。

**示例:**

> **输入:**arr[]= {“100”、“1001”、“0011”}
> **输出:** 1110
> 0100 **异或** 1001 **异或** 0011 = 1110
> 
> **输入:**arr[]= {“10”、“11”、“1000001”}
> T3】输出: 1000000

**进场:**

*   **第一步:**首先找到最大大小的二进制字符串。
*   **第二步:**通过在 [**最高有效位**](https://www.geeksforgeeks.org/find-significant-set-bit-number/) 上加 0，使数组中的所有二进制字符串达到最大字符串的大小
*   **步骤 3:** 现在通过对数组中的所有二进制字符串执行[按位异或](https://www.geeksforgeeks.org/tag/xor/)来查找结果字符串。

**例如:**

1.  让二进制数组为{“100”、“001”和“1111”}。
2.  这里最大的二进制字符串是 4。
3.  通过在 MSB 处添加 0，使数组中的所有二进制字符串的大小都为 4。现在二进制数组变成了{“0100”、“0001”和“1111”}
4.  对数组中的所有二进制字符串执行[位异或](https://www.geeksforgeeks.org/tag/xor/)

```
“0100” XOR “0001” XOR “1111” = “1110”
```

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the bitwise XOR
// of all the binary strings
void strBitwiseXOR(string* arr, int n)
{
    string result;

    int max_len = INT_MIN;

    // Get max size and reverse each string
    // Since we have to perform XOR operation
    // on bits from right to left
    // Reversing the string will make it easier
    // to perform operation from left to right
    for (int i = 0; i < n; i++) {
        max_len = max(max_len,
                      (int)arr[i].size());
        reverse(arr[i].begin(),
                arr[i].end());
    }

    for (int i = 0; i < n; i++) {

        // Add 0s to the end
        // of strings if needed
        string s;
        for (int j = 0;
             j < max_len - arr[i].size();
             j++)
            s += '0';

        arr[i] = arr[i] + s;
    }

    // Perform XOR operation on each bit
    for (int i = 0; i < max_len; i++) {
        int pres_bit = 0;

        for (int j = 0; j < n; j++)
            pres_bit = pres_bit ^ (arr[j][i] - '0');

        result += (pres_bit + '0');
    }

    // Reverse the resultant string
    // to get the final string
    reverse(result.begin(), result.end());

    // Return the final string
    cout << result;
}

// Driver code
int main()
{
    string arr[] = { "1000", "10001", "0011" };
    int n = sizeof(arr) / sizeof(arr[0]);

    strBitwiseXOR(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;
import java.util.*;

class GFG{

// Function to return the
// reverse string
static String reverse(String str)
{
    String rev = "";
    for(int i = str.length() - 1; i >= 0; i--)
        rev = rev + str.charAt(i);

    return rev;
}

// Function to return the bitwise XOR
// of all the binary strings
static String strBitwiseXOR(String[] arr, int n)
{
    String result = "";

    int max_len = Integer.MIN_VALUE;

    // Get max size and reverse each string
    // Since we have to perform XOR operation
    // on bits from right to left
    // Reversing the string will make it easier
    // to perform operation from left to right
    for(int i = 0; i < n; i++)
    {
        max_len = Math.max(max_len,
                  (int)arr[i].length());
        arr[i] = reverse(arr[i]);
    }

    for(int i = 0; i < n; i++)
    {

        // Add 0s to the end
        // of strings if needed
        String s = "";
        for(int j = 0;
                j < max_len - arr[i].length();
                j++)
            s += '0';

        arr[i] = arr[i] + s;
    }

    // Perform XOR operation on each bit
    for(int i = 0; i < max_len; i++)
    {
        int pres_bit = 0;

        for(int j = 0; j < n; j++)
            pres_bit = pres_bit ^
                      (arr[j].charAt(i) - '0');

        result += (char)(pres_bit + '0');
    }

    // Reverse the resultant string
    // to get the final string
    result = reverse(result);

    // Return the final string
    return result;
}

// Driver code
public static void main(String[] args)
{
    String[] arr = { "1000", "10001", "0011" };
    int n = arr.length;

    System.out.print(strBitwiseXOR(arr, n));
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Function to return the bitwise XOR
# of all the binary strings
import sys
def strBitwiseXOR(arr, n):
    result = ""
    max_len = -1

    # Get max size and reverse each string
    # Since we have to perform XOR operation
    # on bits from right to left
    # Reversing the string will make it easier
    # to perform operation from left to right
    for i in range(n):
        max_len = max(max_len, len(arr[i]))
        arr[i] = arr[i][::-1]

    for i in range(n):
        # Add 0s to the end
        # of strings if needed
        s = ""
        # t = max_len - len(arr[i])
        for j in range(max_len - len(arr[i])):
            s += "0"

        arr[i] = arr[i] + s

    # Perform XOR operation on each bit
    for i in range(max_len):
        pres_bit = 0

        for j in range(n):
            pres_bit = pres_bit ^ (ord(arr[j][i]) - ord('0'))

        result += chr((pres_bit) + ord('0'))

    # Reverse the resultant string
    # to get the final string
    result = result[::-1]

    # Return the final string
    print(result)

# Driver code
if(__name__ == "__main__"):
    arr = ["1000", "10001", "0011"]
    n = len(arr)
    strBitwiseXOR(arr, n)

# This code is contributed by skylags
```

## C#

```
// C# implementation of the approach
using System;

class GFG{

// Function to return the
// reverse string
static string reverse(string str)
{
    string rev = "";
    for(int i = str.Length - 1; i >= 0; i--)
        rev = rev + str[i];

    return rev;
}

// Function to return the bitwise XOR
// of all the binary strings
static string strBitwiseXOR(string[] arr, int n)
{
    string result = "";

    int max_len = int.MinValue;

    // Get max size and reverse each string
    // Since we have to perform XOR operation
    // on bits from right to left
    // Reversing the string will make it easier
    // to perform operation from left to right
    for(int i = 0; i < n; i++)
    {
        max_len = Math.Max(max_len,
                          (int)arr[i].Length);
        arr[i] = reverse(arr[i]);
    }

    for(int i = 0; i < n; i++)
    {

        // Add 0s to the end
        // of strings if needed
        string s = "";
        for(int j = 0;
                j < max_len - arr[i].Length;
                j++)
            s += '0';

        arr[i] = arr[i] + s;
    }

    // Perform XOR operation on each bit
    for(int i = 0; i < max_len; i++)
    {
        int pres_bit = 0;

        for(int j = 0; j < n; j++)
            pres_bit = pres_bit ^
                       (arr[j][i] - '0');

        result += (char)(pres_bit + '0');
    }

    // Reverse the resultant string
    // to get the final string
    result = reverse(result);

    // Return the final string
    return result;
}

// Driver code
public static void Main()
{
    string[] arr = { "1000", "10001", "0011" };
    int n = arr.Length;

    Console.Write(strBitwiseXOR(arr, n));
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the bitwise XOR
// of all the binary strings
function strBitwiseXOR(arr, n)
{
    var result = "";

    var max_len = -1000000000;

    // Get max size and reverse each string
    // Since we have to perform XOR operation
    // on bits from right to left
    // Reversing the string will make it easier
    // to perform operation from left to right
    for (var i = 0; i < n; i++) {
        max_len = Math.max(max_len,
                       arr[i].length);
        arr[i] = arr[i].split('').reverse().join('');
    }

    for (var i = 0; i < n; i++) {

        // Add 0s to the end
        // of strings if needed
        var s;
        for (var j = 0;
             j < max_len - arr[i].length;
             j++)
            s += '0';

        arr[i] = arr[i] + s;
    }

    // Perform XOR operation on each bit
    for (var i = 0; i < max_len; i++) {
        var pres_bit = 0;

        for (var j = 0; j < n; j++)
            pres_bit = pres_bit ^ (arr[j][i] - '0'.charCodeAt(0));

        result += (pres_bit + '0'.charCodeAt(0));
    }

    // Reverse the resultant string
    // to get the final string
    result = result.split('').reverse().join('');

    // Return the final string
    document.write( result);
}

// Driver code
var arr = ["1000", "10001", "0011"];
var n = arr.length;
strBitwiseXOR(arr, n);

</script>
```

**Output:** 

```
11010
```