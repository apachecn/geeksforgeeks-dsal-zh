# 生成字典最小的 0、1 和 2 字符串，允许相邻交换

> 原文:[https://www . geeksforgeeks . org/generate-按字典顺序排列-允许 0-1 和 2 的最小字符串与相邻字符串互换/](https://www.geeksforgeeks.org/generate-lexicographically-smallest-string-of-0-1-and-2-with-adjacent-swaps-allowed/)

给定仅包含字符 **0** 、 **1** 和 **2** 的字符串**字符串**，您可以交换任意两个相邻(连续)字符 **0** 和 **1** 或任意两个相邻(连续)字符 **1** 和 **2** 。任务是通过使用这些交换任意次数来获得最小可能的(字典式的)字符串。
**举例:**

> **输入:**str = " 100210 "
> T3】输出: 001120
> 我们可以交换 0 和 1 或者我们可以交换 1 和 2。不允许交换 0 和 2。所有的互换只能发生在相邻的。
> **输入:** str = "2021"
> **输出:** 1202
> 注意 0 和 2 不能互换

**方式:**您可以将所有的 **1s** 打印在一起，因为 **1** 可以与其他任何一个字符交换，而 **0** 和 **2** 不能交换，因此所有的 **0s** 和 **2s** 将遵循与原始字符串相同的顺序。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the required string
void printString(string str, int n)
{
    // count number of 1s
    int ones = 0;
    for (int i = 0; i < n; i++)
        if (str[i] == '1')
            ones++;

    // To check if the all the 1s
    // have been used or not
    bool used = false;

    for (int i = 0; i < n; i++) {
        if (str[i] == '2' && !used) {
            used = 1;

            // Print all the 1s if any 2 is encountered
            for (int j = 0; j < ones; j++)
                cout << "1";
        }

        // If str[i] = 0 or str[i] = 2
        if (str[i] != '1')
            cout << str[i];
    }

    // If 1s are not printed yet
    if (!used)
        for (int j = 0; j < ones; j++)
            cout << "1";
}

// Driver code
int main()
{
    string str = "100210";
    int n = str.length();
    printString(str, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

// Function to print the required string
static void printString(char[] str, int n)
{
    // count number of 1s
    int ones = 0;
    for (int i = 0; i < n; i++)
        if (str[i] == '1')
            ones++;

    // To check if the all the 1s
    // have been used or not
    boolean used = false;

    for (int i = 0; i < n; i++)
    {
        if (str[i] == '2' && !used)
        {
            used = true;

            // Print all the 1s if any 2 is encountered
            for (int j = 0; j < ones; j++)
                System.out.print("1");
        }

        // If str[i] = 0 or str[i] = 2
        if (str[i] != '1')
            System.out.print(str[i]);

    }

    // If 1s are not printed yet
    if (!used)
        for (int j = 0; j < ones; j++)
            System.out.print("1");
}

// Driver code
public static void main(String[] args)
{
    String str = "100210";
    int n = str.length();
    printString(str.toCharArray(), n);
}
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print the required string
def printString(Str1, n):

    # count number of 1s
    ones = 0
    for i in range(n):
        if (Str1[i] == '1'):
            ones += 1

    # To check if the all the 1s
    # have been used or not
    used = False

    for i in range(n):
        if (Str1[i] == '2' and used == False):
            used = 1

            # Print all the 1s if any 2 is encountered
            for j in range(ones):
                print("1", end = "")

        # If Str1[i] = 0 or Str1[i] = 2
        if (Str1[i] != '1'):
            print(Str1[i], end = "")

    # If 1s are not printed yet
    if (used == False):
        for j in range(ones):
            print("1", end = "")

# Driver code
Str1 = "100210"
n = len(Str1)
printString(Str1, n)

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to print the required string
static void printString(char[] str, int n)
{
    // count number of 1s
    int ones = 0;
    for (int i = 0; i < n; i++)
        if (str[i] == '1')
            ones++;

    // To check if the all the 1s
    // have been used or not
    bool used = false;

    for (int i = 0; i < n; i++)
    {
        if (str[i] == '2' && !used)
        {
            used = true;

            // Print all the 1s if any 2 is encountered
            for (int j = 0; j < ones; j++)
                Console.Write("1");
        }

        // If str[i] = 0 or str[i] = 2
        if (str[i] != '1')
            Console.Write(str[i]);

    }

    // If 1s are not printed yet
    if (!used)
        for (int j = 0; j < ones; j++)
            Console.Write("1");
}

// Driver code
public static void Main(String[] args)
{
    String str = "100210";
    int n = str.Length;
    printString(str.ToCharArray(), n);
}
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to print the required string
function printString($str, $n)
{
    // count number of 1s
    $ones = 0;
    for ($i = 0; $i < $n; $i++)
        if ($str[$i] == '1')
            $ones++;

    // To check if the all the 1s
    // have been used or not
    $used = false;

    for ($i = 0; $i < $n; $i++)
    {
        if ($str[$i] == '2' && !$used)
        {
            $used = 1;

            // Print all the 1s if any 2
            // is encountered
            for ($j = 0; $j < $ones; $j++)
                echo "1";
        }

        // If str[i] = 0 or str[i] = 2
        if ($str[$i] != '1')
            echo $str[$i];
    }

    // If 1s are not printed yet
    if (!$used)
        for ($j = 0; $j < $ones; $j++)
            echo "1";
}

// Driver code
$str = "100210";
$n = strlen($str);
printString($str, $n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    // Function to print the required string
    function printString(str, n)
    {
        // count number of 1s
        let ones = 0;
        for (let i = 0; i < n; i++)
            if (str[i] == '1')
                ones++;

        // To check if the all the 1s
        // have been used or not
        let used = false;

        for (let i = 0; i < n; i++)
        {
            if (str[i] == '2' && !used)
            {
                used = true;

                // Print all the 1s if any 2 is encountered
                for (let j = 0; j < ones; j++)
                    document.write("1");
            }

            // If str[i] = 0 or str[i] = 2
            if (str[i] != '1')
                document.write(str[i]);

        }

        // If 1s are not printed yet
        if (!used)
            for (let j = 0; j < ones; j++)
                document.write("1");
    }

    let str = "100210";
    let n = str.length;
    printString(str.split(''), n);

</script>
```

**Output:** 

```
001120
```