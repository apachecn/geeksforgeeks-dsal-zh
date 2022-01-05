# 通过反转任意子串

检查字符串是否可以在字典上变小

> 原文:[https://www . geesforgeks . org/check-if-string-can-make-按字典顺序-通过反转任意子字符串变小/](https://www.geeksforgeeks.org/check-if-string-can-be-made-lexicographically-smaller-by-reversing-any-substring/)

给定一个字符串 **S** ，任务是检查我们是否可以通过反转给定字符串的任何子字符串来使该字符串在词典上变小。

**示例:**

> **输入:** S = "奋斗者"
> **输出:**是
> 反转“rive”得到字典上更小的“甜叶菊”。
> **输入:** S = "rxz"
> **输出:**否

**接近**:迭代字符串，检查是否有任何索引 **s[i] > s[i + 1]** 。如果至少有一个这样的索引，那么就有可能没有。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if s
// can be made lexicographically smaller
// by reversing a sub-string in s
bool check(string s)
{
    int n = s.size();

    // Traverse in the string
    for (int i = 0; i < n - 1; i++) {

        // Check if s[i+1] < s[i]
        if (s[i] > s[i + 1])
            return true;
    }

    // Not possible
    return false;
}

// Driver code
int main()
{
    string s = "geeksforgeeks";

    if (check(s))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function that returns true if s
// can be made lexicographically smaller
// by reversing a sub-string in s
static boolean check(String s)
{
    int n = s.length();

    // Traverse in the string
    for (int i = 0; i < n - 1; i++)
    {

        // Check if s[i+1] < s[i]
        if (s.charAt(i) > s.charAt(i + 1))
            return true;
    }

    // Not possible
    return false;
}

// Driver code
public static void main(String args[])
{
    String s = "geeksforgeeks";

    if (check(s))
        System.out.println("Yes");
    else
        System.out.println("No");

}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function that returns true if s
# can be made lexicographically smaller
# by reversing a sub-string in s
def check(s):
    n = len(s)

    # Traverse in the string
    for i in range(n-1):

        # Check if s[i+1] < s[i]
        if (s[i] > s[i + 1]):
            return True

    # Not possible
    return False

# Driver code
if __name__ == '__main__':
    s = "geeksforgeeks"

    if (check(s)):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function that returns true if s
// can be made lexicographically smaller
// by reversing a sub-string in s
static bool check(String s)
{
    int n = s.Length;

    // Traverse in the string
    for (int i = 0; i < n - 1; i++)
    {

        // Check if s[i+1] < s[i]
        if (s[i] > s[i + 1])
            return true;
    }

    // Not possible
    return false;
}

// Driver code
public static void Main(String []args)
{
    String s = "geeksforgeeks";

    if (check(s))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");

}
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that returns true if s
// can be made lexicographically smaller
// by reversing a sub-string in s

function check($s)
{
    $n = strlen($s);

    // Traverse in the string
    for ($i = 0; $i < $n - 1; $i++)
    {

        // Check if $s[$i+1] < $s[$i]
        if ($s[$i] > $s[$i + 1])
            return true;
    }

    // Not possible
    return false;
}

    // Driver code
    $s = "geeksforgeeks";

    if (check($s))
    echo "Yes";
    else
        echo "No";

// This code is contributed by jit_t
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function that returns true if s
    // can be made lexicographically smaller
    // by reversing a sub-string in s
    function check(s)
    {
        let n = s.length;

        // Traverse in the string
        for (let i = 0; i < n - 1; i++)
        {

            // Check if s[i+1] < s[i]
            if (s[i] > s[i + 1])
                return true;
        }

        // Not possible
        return false;
    }

    let s = "geeksforgeeks";

    if (check(s))
        document.write("Yes");
    else
        document.write("No");

</script>
```

**Output:** 

```
Yes
```