# 给定字符串中字符纠正的数量，使它们相等

> 原文:[https://www . geesforgeks . org/给定字符串中的字符更正数使其相等/](https://www.geeksforgeeks.org/number-of-character-corrections-in-the-given-strings-to-make-them-equal/)

给定三根弦 **A** 、 **B** 和 **C** 。每一个都是一串由小写英文字母组成的长度 **N** 。任务是通过执行一个操作使所有字符串相等，在这个操作中，给定字符串的任何字符都可以被任何其他字符替换，打印所需的最小操作数。

**示例:**

> **输入:**A =“place”，B =“abcde”，C =“ply be”
> T3】输出:6
> A =“place”，B =“abcde”，C =“ply be”。
> 我们可以通过执行以下六个操作，在最少的操作数内完成任务:
> 将 B 中的第一个字符改为‘p’。B 现在是“pbcde”
> 将 B 中的第二个字符改为‘l’。B 现在是“plcde”
> 将 B 和 C 中的第三个字符改为‘a’。b 和 C 现在分别是“plade”和“plabe”。
> 将 B 中的第四个字符改为‘c’。b 现在是“place”
> 将 C 中的第四个字符改为‘C’。C 现在是【地点】
> **输入:** A =“游戏”，B =“游戏”，C =“游戏”
> **输出:** 0

**方法:**运行一个循环，检查所有字符串的**I<sup>th</sup>T5】字符是否相等，然后不需要任何操作。如果两个字符相等，则需要一个操作，如果三个字符都不同，则需要两个操作。** 

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of operations required
const int minOperations(int n, string a, string b, string c)
{

    // To store the count of operations
    int ans = 0;
    for (int i = 0; i < n; i++)
    {
        char x = a[i];
        char y = b[i];
        char z = c[i];

        // No operation required
        if (x == y && y == z)
            ;

        // One operation is required when
        // any two characters are equal
        else if (x == y || y == z || x == z)
        {
            ans++;
        }

        // Two operations are required when
        // none of the characters are equal
        else
        {
            ans += 2;
        }
    }

    // Return the minimum count of operations required
    return ans;
}

// Driver code
int main()
{
    string a = "place";
    string b = "abcde";
    string c = "plybe";
    int n = a.size();
    cout << minOperations(n, a, b, c);
    return 0;
}

// This code is contributed by 29AjayKumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the count of operations required
    static int minOperations(int n, String a, String b, String c)
    {

        // To store the count of operations
        int ans = 0;
        for (int i = 0; i < n; i++) {
            char x = a.charAt(i);
            char y = b.charAt(i);
            char z = c.charAt(i);

            // No operation required
            if (x == y && y == z)
                ;

            // One operation is required when
            // any two characters are equal
            else if (x == y || y == z || x == z) {
                ans++;
            }

            // Two operations are required when
            // none of the characters are equal
            else {
                ans += 2;
            }
        }

        // Return the minimum count of operations required
        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        String a = "place";
        String b = "abcde";
        String c = "plybe";
        int n = a.length();
        System.out.print(minOperations(n, a, b, c));
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the count
# of operations required
def minOperations(n, a, b, c):

    # To store the count of operations
    ans = 0
    for i in range(n):
        x = a[i]
        y = b[i]
        z = c[i]

        # No operation required
        if (x == y and y == z):
            continue

        # One operation is required when
        # any two characters are equal
        elif (x == y or y == z or x == z):
            ans += 1

        # Two operations are required when
        # none of the characters are equal
        else:
            ans += 2

    # Return the minimum count
    # of operations required
    return ans

# Driver code
if __name__ == '__main__':
    a = "place"
    b = "abcde"
    c = "plybe"
    n = len(a)
    print(minOperations(n, a, b, c))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the count of operations required
    static int minOperations(int n, string a, string b, string c)
    {

        // To store the count of operations
        int ans = 0;
        for (int i = 0; i < n; i++)
        {
            char x = a[i];
            char y = b[i];
            char z = c[i];

            // No operation required
            if (x == y && y == z)
                {;}

            // One operation is required when
            // any two characters are equal
            else if (x == y || y == z || x == z)
            {
                ans++;
            }

            // Two operations are required when
            // none of the characters are equal
            else
            {
                ans += 2;
            }
        }

        // Return the minimum count of operations required
        return ans;
    }

    // Driver code
    public static void Main()
    {
        string a = "place";
        string b = "abcde";
        string c = "plybe";
        int n = a.Length;
        Console.Write(minOperations(n, a, b, c));
    }
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count of 
// operations required
function minOperations($n, $a, $b, $c)
{

    // To store the count of operations
    $ans = 0;
    for ($i = 0; $i < $n; $i++)
    {
        $x = $a[$i];
        $y = $b[$i];
        $z = $c[$i];

        // No operation required
        if ($x == $y && $y == $z)
            ;

        // One operation is required when
        // any two characters are equal
        else if ($x == $y ||
                 $y == $z || $x == $z)
        {
            $ans++;
        }

        // Two operations are required when
        // none of the characters are equal
        else
        {
            $ans += 2;
        }
    }

    // Return the minimum count of
    // operations required
    return $ans;
}

// Driver code
$a = "place";
$b = "abcde";
$c = "plybe";
$n = strlen($a);
echo minOperations($n, $a, $b, $c);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the count of operations required
    function minOperations(n, a, b, c)
    {

        // To store the count of operations
        let ans = 0;
        for (let i = 0; i < n; i++)
        {
            let x = a[i];
            let y = b[i];
            let z = c[i];

            // No operation required
            if (x == y && y == z)
                {;}

            // One operation is required when
            // any two characters are equal
            else if (x == y || y == z || x == z)
            {
                ans++;
            }

            // Two operations are required when
            // none of the characters are equal
            else
            {
                ans += 2;
            }
        }

        // Return the minimum count of operations required
        return ans;
    }

    let a = "place";
    let b = "abcde";
    let c = "plybe";
    let n = a.length;
    document.write(minOperations(n, a, b, c));

</script>
```

**Output:** 

```
6
```