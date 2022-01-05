# 生成所有长度为 N 的二进制字符串，0 和 1 的计数相等

> 原文:[https://www . geesforgeks . org/generate-all-binary-length-n-with-count-0s-1s/](https://www.geeksforgeeks.org/generate-all-binary-strings-of-length-n-with-equal-count-of-0s-and-1s/)

给定一个整数 **N** ，任务是生成所有**二进制**字符串，其中**等于**T6】0s 和 **1s** 。如果没有字符串，打印 **-1**

**示例:**

> **输入** : N = 2
> **输出:**【01】【10】
> **解释**:长度为 2 的所有可能的二进制字符串为:01、10、11、00。其中，只有 2 个具有相同数量的 0 和 1
> 
> **输入:** 4
> **输出:**“0011”“0101”“0110”“1100”“1010”“1001”

**方法:**使用[递归可以解决任务。](http://www.geeksforgeeks.org/recursion/)如果 **N** 为**奇数**，那么答案为 **-1** ，否则，我们可以使用**递归**生成所有**等于**0 和 1 的二进制字符串。按照以下步骤解决问题:
[](http://www.geeksforgeeks.org/recursion/)

*   变量**1**记录字符串中**1**的数量，变量**0**记录字符串中**0**的数量。
*   **1**和**0**都应该有频率 **N/2** 。
*   **基础条件:**字符串 **s** 存储**输出**字符串。因此，当 s 的长度达到 **N** 时，我们停止递归调用并打印输出字符串 s **。**
*   如果 **1 的**的**频率**小于的 **N/2** ，则将 **1** 加到弦上，**递增 1**。
*   如果 **0 的**的**频率**小于的 **N/2** ，则在字符串中添加 **0** ，并且**递增零**。

下面是上述代码的实现:

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Recursive function that prints
// all strings of N length with equal 1's and 0's
void binaryNum(int n, string s, int ones,
               int zeros)
{

    // String s contains the output to be printed
    // ones stores the frequency of 1's
    // zeros stores the frequency of 0's
    // Base Condition: When the length of string s
    // becomes N
    if (s.length() == n)
    {
        cout << (s) << endl;
        return;
    }

    // If frequency of 1's is less than N/2 then
    // add 1 to the string and increment ones
    if (ones < n / 2)
        binaryNum(n, s + "1", ones + 1, zeros);

    // If frequency of 0's is less than N/2 then
    // add 0 to the string and increment zeros
    if (zeros < n / 2)
        binaryNum(n, s + "0", ones, zeros + 1);
}

// Driver Code
int main()
{

    string s = "";
    binaryNum(4, s, 0, 0);
    return 0;
}

// This code is contributed by Potta Lokesh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

    // Recursive function that prints
    // all strings of N length with equal 1's and 0's
    static void binaryNum(int n, String s, int ones,
                          int zeros)
    {
        // String s contains the output to be printed
        // ones stores the frequency of 1's
        // zeros stores the frequency of 0's
        // Base Condition: When the length of string s
        // becomes N
        if (s.length() == n) {
            System.out.println(s);
            return;
        }

        // If frequency of 1's is less than N/2 then
        // add 1 to the string and increment ones
        if (ones < n / 2)
            binaryNum(n, s + "1", ones + 1, zeros);

        // If frequency of 0's is less than N/2 then
        // add 0 to the string and increment zeros
        if (zeros < n / 2)
            binaryNum(n, s + "0", ones, zeros + 1);
    }

    // Driver Code
    public static void main(String[] args)
    {
        String s = "";
        binaryNum(4, s, 0, 0);
    }
}
```

## 蟒蛇 3

```
# python code for the above approach

# Recursive function that prints
# all strings of N length with equal 1's and 0's
def binaryNum(n, s, ones, zeros):

    # String s contains the output to be printed
    # ones stores the frequency of 1's
    # zeros stores the frequency of 0's
    # Base Condition: When the length of string s
    # becomes N
    if (len(s) == n):

        print(s)
        return

    # If frequency of 1's is less than N/2 then
    # add 1 to the string and increment ones
    if (ones < n / 2):
        binaryNum(n, s + "1", ones + 1, zeros)

    # If frequency of 0's is less than N/2 then
    # add 0 to the string and increment zeros
    if (zeros < n / 2):
        binaryNum(n, s + "0", ones, zeros + 1)

# Driver Code
if __name__ == "__main__":

    s = ""
    binaryNum(4, s, 0, 0)

# This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;

class GFG {

    // Recursive function that prints
    // all strings of N length with equal 1's and 0's
    static void binaryNum(int n, string s, int ones,
                          int zeros)
    {
        // String s contains the output to be printed
        // ones stores the frequency of 1's
        // zeros stores the frequency of 0's
        // Base Condition: When the length of string s
        // becomes N
        if (s.Length == n) {
            Console.WriteLine(s);
            return;
        }

        // If frequency of 1's is less than N/2 then
        // add 1 to the string and increment ones
        if (ones < n / 2)
            binaryNum(n, s + "1", ones + 1, zeros);

        // If frequency of 0's is less than N/2 then
        // add 0 to the string and increment zeros
        if (zeros < n / 2)
            binaryNum(n, s + "0", ones, zeros + 1);
    }

    // Driver Code
    public static void Main(string[] args)
    {
        string s = "";
        binaryNum(4, s, 0, 0);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
// javascript program for the above approach

   // Recursive function that prints
    // all strings of N length with equal 1's and 0's
    function binaryNum(n, s, ones, zeros)
    {

        // String s contains the output to be printed
        // ones stores the frequency of 1's
        // zeros stores the frequency of 0's
        // Base Condition: When the length of string s
        // becomes N
        if (s.length == n) {
            document.write(s+"<br>");
            return;
        }

        // If frequency of 1's is less than N/2 then
        // add 1 to the string and increment ones
        if (ones < n / 2)
            binaryNum(n, s + "1", ones + 1, zeros);

        // If frequency of 0's is less than N/2 then
        // add 0 to the string and increment zeros
        if (zeros < n / 2)
            binaryNum(n, s + "0", ones, zeros + 1);
    }

// Driver Code
var s = "";
binaryNum(4, s, 0, 0);

// This code is contributed by 29AjayKumar
</script>
```

**Output**

```
1100
1010
1001
0110
0101
0011
```

***时间复杂度***:O(2<sup>N</sup>)
***辅助空间*** : O(1)