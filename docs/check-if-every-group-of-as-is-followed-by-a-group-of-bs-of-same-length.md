# 检查每组 a 后面是否跟有一组相同长度的 b

> 原文:[https://www . geesforgeks . org/check-if-每一组 as-as-后跟一组相同长度的 bs/](https://www.geeksforgeeks.org/check-if-every-group-of-as-is-followed-by-a-group-of-bs-of-same-length/)

给定字符串 **str** ，任务是检查每组连续的 **a 的**后面是否跟有一组相同长度的连续的 **b 的**。如果每组条件为真，则打印 **1** 否则打印 **0** 。
**举例:**

> **输入:**str = " abababb "
> T3】输出: 1
> ab，ab，aabb。所有组均有效
> **输入:** str = "aabbabb"
> **输出:** 0
> aabb，abb(单个‘A’后跟 2 个‘b’)

**进场:**

*   对于字符串中的每一个 **a** ，递增**计数**。
*   从第一个 **b** 开始，递减每个 **b** 的计数。
*   如果在上述周期结束时，**计数！= 0** 则返回**假**。
*   否则，对字符串的其余部分重复前两步。
*   如果所有周期都满足条件，返回**真**，否则打印 **0** 。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to match whether there are always n consecutive b's
// followed by n consecutive a's throughout the string
int matchPattern(string s)
{
    int count = 0;
    int n = s.length();

    // Traverse through the string
    int i = 0;
    while (i < n) {

        // Count a's in current segment
        while (i < n && s[i] == 'a') {
            count++;
            i++;
        }

        // Count b's in current segment
        while (i < n && s[i] == 'b') {
            count--;
            i++;
        }

        // If both counts are not same.
        if (count != 0)
            return false;
    }

    return true;
}

// Driver code
int main()
{
    string s = "bb";
    if (matchPattern(s) == true)
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

public class GFG{

// Function to match whether there are always n consecutive b's
// followed by n consecutive a's throughout the string
static boolean matchPattern(String s)
{
    int count = 0;
    int n = s.length();

    // Traverse through the string
    int i = 0;
    while (i < n) {

        // Count a's in current segment
        while (i < n && s.charAt(i) == 'a') {
            count++;
            i++;
        }

        // Count b's in current segment
        while (i < n && s.charAt(i) == 'b') {
            count--;
            i++;
        }

        // If both counts are not same.
        if (count != 0)
            return false;
    }

    return true;
}

// Driver code
public static void main(String []args)
{
    String s = "bb";
    if (matchPattern(s) == true)
        System.out.println("Yes");
    else
        System.out.println("No");
}

// This code is contributed by Ryuga
}
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to match whether there are
# always n consecutive b's followed by
# n consecutive a's throughout the string
def matchPattern(s):

    count = 0;
    n = len(s);

    # Traverse through the string
    i = 0;
    while (i < n) :

        # Count a's in current segment
        while (i < n and s[i] == 'a'):

            count += 1 ;
            i =+ 1;

        # Count b's in current segment
        while (i < n and s[i] == 'b'):
            count -= 1 ;
            i += 1;

        # If both counts are not same.
        if (count != 0):
            return False;

    return True;

# Driver code
s = "bb";
if (matchPattern(s) == True):
    print("Yes");
else:
    print("No");

# This code is contributed
# by Akanksha Rai
```

## C#

```
// C# implementation of the above approach

using System;
public class GFG{

// Function to match whether there are always n consecutive b's
// followed by n consecutive a's throughout the string
static bool matchPattern(string s)
{
    int count = 0;
    int n = s.Length;

    // Traverse through the string
    int i = 0;
    while (i < n) {

        // Count a's in current segment
        while (i < n && s[i] == 'a') {
            count++;
            i++;
        }

        // Count b's in current segment
        while (i < n && s[i] == 'b') {
            count--;
            i++;
        }

        // If both counts are not same.
        if (count != 0)
            return false;
    }

    return true;
}

// Driver code
public static void Main()
{
    string s = "bb";
    if (matchPattern(s) == true)
        Console.Write("Yes");
    else
        Console.Write("No");
}

}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
//PHP implementation of the approach

// Function to match whether there are always n consecutive b's
// followed by n consecutive a's throughout the string
function  matchPattern($s)
{
    $count = 0;
    $n = strlen($s);

    // Traverse through the string
    $i = 0;
    while ($i < $n) {

        // Count a's in current segment
        while ($i < $n && $s[$i] == 'a') {
            $count++;
            $i++;
        }

        // Count b's in current segment
        while ($i < $n && $s[$i] == 'b') {
            $count--;
            $i++;
        }

        // If both counts are not same.
        if ($count != 0)
            return false;
    }

    return true;
}

// Driver code

    $s = "bb";
    if (matchPattern($s) == true)
        echo  "Yes";
    else
        echo "No";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

    // Javascript implementation of
    // the above approach

    // Function to match whether there are
    // always n consecutive b's
    // followed by n consecutive a's
    // throughout the string
    function matchPattern(s)
    {
        let count = 0;
        let n = s.length;

        // Traverse through the string
        let i = 0;
        while (i < n)
        {

            // Count a's in current segment
            while (i < n && s[i] == 'a')
            {
                count++;
                i++;
            }

            // Count b's in current segment
            while (i < n && s[i] == 'b')
            {
                count--;
                i++;
            }

            // If both counts are not same.
            if (count != 0)
                return false;
        }

        return true;
    }

    let s = "bb";
    if (matchPattern(s) == true)
        document.write("Yes");
    else
        document.write("No");

</script>
```

**Output:** 

```
No
```