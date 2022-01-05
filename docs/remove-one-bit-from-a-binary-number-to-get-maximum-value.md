# 从二进制数中去掉一位，得到最大值

> 原文:[https://www . geesforgeks . org/从二进制数中移除一位以获得最大值/](https://www.geeksforgeeks.org/remove-one-bit-from-a-binary-number-to-get-maximum-value/)

给定一个二进制数，任务是从中删除一位，这样在删除后，所有选项中得到的二进制数最大。
**例:**

```
Input: 110
Output: 11
    As 110 = 6 in decimal, 
    the option is to remove either 0 or 1.
    So the possible combinations are 10, 11
    The max number is 11 = 3 in decimal.  

Input:1001
Output: 101
```

**进场:**

1.  从左到右遍历二进制数。
2.  找到冗余最少的 0 位，因为该位对结果二进制数的影响最小。
3.  跳过这一点，或者去掉它。
4.  其余位给出最大值二进制数。

以下是上述方法的实施:
**程序:**

## C++

```
// C++ program to find next maximum binary number
// with one bit removed

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum binary number
int printMaxAfterRemoval(string s)
{
    bool flag = false;
    int n = s.length();

    // Traverse the binary number
    for (int i = 0; i < n; i++) {

        // Try finding a 0 and skip it
        if (s[i] == '0' && flag == false) {
            flag = true;
            continue;
        }
        else
            cout << s[i];
    }
}

// Driver code
int main()
{

    // Get the binary number
    string s = "1001";

    // Find the maximum binary number
    printMaxAfterRemoval(s);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find next maximum binary number
// with one bit removed

import java.io.*;

class GFG {

// Function to find the maximum binary number
static int printMaxAfterRemoval(String s)
{
    boolean flag = false;
    int n = s.length();

    // Traverse the binary number
    for (int i = 0; i < n; i++) {

        // Try finding a 0 and skip it
        if (s.charAt(i) == '0' && flag == false) {
            flag = true;
            continue;
        }
        else
            System.out.print( s.charAt(i));
    }
  return 0;
}

// Driver code
    public static void main (String[] args) {
            // Get the binary number
    String s = "1001";

    // Find the maximum binary number
    printMaxAfterRemoval(s);
    }
}
// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python3 program to find next maximum 
# binary number with one bit removed

# Function to find the maximum
# binary number
def printMaxAfterRemoval(s):

    flag = False
    n = len(s)

    # Traverse the binary number
    for i in range(0, n):

        # Try finding a 0 and skip it
        if s[i] == '0' and flag == False:
            flag = True
            continue

        else:
            print(s[i], end = "")

# Driver code
if __name__ == "__main__":

    # Get the binary number
    s = "1001"

    # Find the maximum binary number
    printMaxAfterRemoval(s)

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# program to find next maximum
// binary number with one bit removed
using System;

class GFG
{
// Function to find the maximum
// binary number
static int printMaxAfterRemoval(String s)
{
    bool flag = false;
    int n = s.Length;

    // Traverse the binary number
    for (int i = 0; i < n; i++)
    {

        // Try finding a 0 and skip it
        if (s[i] == '0' && flag == false)
        {
            flag = true;
            continue;
        }
        else
            Console.Write(s[i]);
    }
    return 0;
}

// Driver Code
static void Main()
{
    // Get the binary number
    String s = "1001";

    // Find the maximum binary number
    printMaxAfterRemoval(s);
}
}

// This code is contributed by Ryuga.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find next maximum
// binary number with one bit removed

// Function to find the maximum
// binary number
function printMaxAfterRemoval($s)
{
    $flag = false;
    $n = strlen($s);

    // Traverse the binary number
    for ($i = 0; $i < $n; $i++)
    {

        // Try finding a 0 and skip it
        if ($s[$i] == '0' && $flag == false)
        {
            $flag = true;
            continue;
        }
        else
            echo $s[$i];
    }
}

// Driver code

// Get the binary number
$s = "1001";

// Find the maximum binary number
printMaxAfterRemoval($s);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>   
    // Javascript program to find next maximum
    // binary number with one bit removed

    // Function to find the maximum
    // binary number
    function printMaxAfterRemoval(s)
    {
        let flag = false;
        let n = s.length;

        // Traverse the binary number
        for (let i = 0; i < n; i++)
        {

            // Try finding a 0 and skip it
            if (s[i] == '0' && flag == false)
            {
                flag = true;
                continue;
            }
            else
                document.write(s[i]);
        }
        return 0;
    }

    // Get the binary number
    let s = "1001";

    // Find the maximum binary number
    printMaxAfterRemoval(s);

</script>
```

**Output:** 

```
101
```

**时间复杂度:** O(n)