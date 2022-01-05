# 最长平衡括号前缀的长度

> 原文:[https://www . geesforgeks . org/length-最长-平衡-括号-前缀/](https://www.geeksforgeeks.org/length-longest-balanced-parentheses-prefix/)

给定一串左括号“(”和右括号“)”。任务是找到最长平衡前缀的长度。
示例:

```
Input : S = "((()())())((" 
Output : 10
From index 0 to index 9, they are forming 
a balanced parentheses prefix.

Input : S = "()(())((()"
Output : 6
```

其思想是将左括号“(”的值作为 1，右括号“)”的值作为-1。现在开始寻找给定字符串的前缀和。最远的索引，比如 maxi，其中 sum 的值为 0，是存在最长平衡前缀的索引。所以答案是 maxi + 1。
以下是该方法的实现:

## C++

```
// CPP Program to find length of longest balanced
// parentheses prefix.
#include <bits/stdc++.h>
using namespace std;

// Return the length of longest balanced parentheses
// prefix.
int maxbalancedprefix(char str[], int n)
{
    int sum = 0;
    int maxi = 0;

    // Traversing the string.
    for (int i = 0; i < n; i++) {

        // If open bracket add 1 to sum.
        if (str[i] == '(')
            sum += 1;

        // If closed bracket subtract 1
        // from sum
        else
            sum -= 1;

        // if first bracket is closing bracket
        // then this condition would help
        if (sum < 0)
            break;

        // If sum is 0, store the index
        // value.
        if (sum == 0)
            maxi = i + 1;
    }

    return maxi;
}

// Driven Program
int main()
{
    char str[] = "((()())())((";
    int n = strlen(str);

    cout << maxbalancedprefix(str, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find length of longest
// balanced parentheses prefix.
import java.io.*;

class GFG {

    // Return the length of longest
    // balanced parentheses prefix.
    static int maxbalancedprefix(String str, int n)
    {
        int sum = 0;
        int maxi = 0;

        // Traversing the string.
        for (int i = 0; i < n; i++) {

            // If open bracket add 1 to sum.
            if (str.charAt(i) == '(')
                sum += 1;

            // If closed bracket subtract 1
            // from sum
            else
                sum -= 1;

            // if first bracket is closing bracket
            // then this condition would help
            if (sum < 0)
                break;

            // If sum is 0, store the index
            // value.
            if (sum == 0)
                maxi = i + 1;
        }

        return maxi;
    }

    // Driven Program
    public static void main(String[] args)
    {
        String str = "((()())())((";
        int n = str.length();

        System.out.println(maxbalancedprefix(str, n));
    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python3 code to find length of
# longest balanced parentheses prefix.

# Function to return the length of
# longest balanced parentheses prefix.
def maxbalancedprefix (str, n):
    _sum = 0
    maxi = 0

    # Traversing the string.
    for i in range(n):

        # If open bracket add 1 to sum.
        if str[i] == '(':
            _sum += 1

        # If closed bracket subtract 1
        # from sum
        else:
            _sum -= 1

       # if first bracket is closing bracket
       # then this condition would help
        if _sum < 0:
            break

        # If sum is 0, store the
        # index value.
        if _sum == 0:
            maxi = i + 1
    return maxi

# Driver Code
str = '((()())())(('
n = len(str)
print(maxbalancedprefix (str, n))

# This code is contributed by "Abhishek Sharma 44"
```

## C#

```
// C# Program to find length of longest
// balanced parentheses prefix.
using System;

class GFG {

    // Return the length of longest
    // balanced parentheses prefix.
    static int maxbalancedprefix(string str, int n)
    {
        int sum = 0;
        int maxi = 0;

        // Traversing the string.
        for (int i = 0; i < n; i++) {

            // If open bracket add 1 to sum.
            if (str[i] == '(')
                sum += 1;

            // If closed bracket subtract 1
            // from sum
            else
                sum -= 1;

            // if first bracket is closing bracket
            // then this condition would help
            if (sum < 0)
                break;

            // If sum is 0, store the index
            // value.
            if (sum == 0)
                maxi = i + 1;
        }

        return maxi;
    }

    // Driven Program
    public static void Main()
    {
        string str = "((()())())((";
        int n = str.Length;

        Console.WriteLine(maxbalancedprefix(str, n));
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find length
// of longest balanced
// parentheses prefix.

// Return the length of longest
// balanced parentheses prefix.
function maxbalancedprefix($str, $n)
{
    $sum = 0;
    $maxi = 0;

    // Traversing the string.
    for ($i = 0; $i <$n; $i++) {

        // If open bracket add 1 to sum.
        if ($str[$i] == '(')
            $sum += 1;

        // If closed bracket subtract 1
        // from sum
        else
            $sum -= 1;

        if ($sum < 0)
            break;

        // If sum is 0, store the index
        // value.
        if ($sum == 0)
            $maxi = $i+1;
    }

    return $maxi;
}

// Driver Code
$str = array('(', '(', '(', ')', '(', ')', ')', '(', ')', ')', '(', '(');
$n = count($str);

echo maxbalancedprefix($str, $n);

// This code is contributed by anuj_67..
?>
```

## java 描述语言

```
<script>

// Javascript Program to find
// length of longest balanced
// parentheses prefix.

// Return the length of longest
// balanced parentheses
// prefix.
function maxbalancedprefix( str, n)
{
    var sum = 0;
    var maxi = 0;

    // Traversing the string.
    for (var i = 0; i < n; i++) {

        // If open bracket add 1 to sum.
        if (str[i] == '(')
            sum += 1;

        // If closed bracket subtract 1
        // from sum
        else
            sum -= 1;

        // if first bracket is closing bracket
        // then this condition would help
        if (sum < 0)
            break;

        // If sum is 0, store the index
        // value.
        if (sum == 0)
            maxi = i + 1;
    }

    return maxi;
}

// Driven Program
var str = "((()())())((";
var n = str.length;
document.write( maxbalancedprefix(str, n));

</script>
```

**输出:**

```
10
```